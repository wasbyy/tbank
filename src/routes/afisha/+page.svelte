<script lang="ts">
  import { onMount } from 'svelte';

  let avatar = '/avatar.png';
  let isLoading = true;
  let error = null;
  
  // Добавляем параметры для фильтрации и сортировки
  let selectedTag = 'Любой';
  let selectedSort = 'Сначала новые';
  
  interface GalleryImage {
    id: number;
    event_id: number;
    image_url: string;
    description: string | null;
    created_at: string;
  }
  
  interface Event {
    id: number;
    title: string;
    description: string;
    start_date: string;
    end_date: string;
    price: number;
    max_participants: number;
    is_team_event: boolean;
    location: string;
    created_at: string;
    participants: number[];
    // Добавляем поля для отображения в интерфейсе
    image?: string;
    tag?: string;
    images?: GalleryImage[]; // Массив изображений из галереи
  }

  let events: Event[] = [];
  let filteredEvents: Event[] = [];
  
  // Функция для форматирования даты
  function formatDate(dateString: string): string {
    const date = new Date(dateString);
    return date.toLocaleDateString('ru-RU', { 
      day: 'numeric', 
      month: 'long', 
      year: 'numeric' 
    });
  }
  
  // Функция для получения тега на основе описания
  function getTagFromDescription(description: string): string {
    if (description.toLowerCase().includes('универсиад')) return '#Универсиада';
    if (description.toLowerCase().includes('конференц')) return '#Конференция';
    if (description.toLowerCase().includes('олимпиад')) return '#Олимпиада';
    if (description.toLowerCase().includes('мгу')) return '#Университетская жизнь';
    return '#Мероприятие';
  }
  
  // Функция для получения картинки на основе тега (запасной вариант)
  function getImageByTag(tag: string): string {
    switch (tag) {
      case '#Универсиада':
        return '/event1.svg';
      case '#Университетская жизнь':
        return '/event2.svg';
      case '#Конференция':
        return '/event3.svg';
      case '#Олимпиада':
        return '/event4.svg';
      default:
        return '/event1.svg';
    }
  }

  // Функция для загрузки изображений для конкретного события
  async function loadEventImages(eventId: number): Promise<GalleryImage[]> {
    try {
      const response = await fetch(`http://localhost:8000/gallery?event_id=${eventId}`);
      if (!response.ok) {
        throw new Error(`Ошибка при загрузке изображений: ${response.status}`);
      }
      return await response.json();
    } catch (error) {
      console.error(`Ошибка загрузки изображений для события ${eventId}:`, error);
      return [];
    }
  }

  // Применение фильтров и сортировки
  function applyFiltersAndSort() {
    let result = [...events];
    
    // Применяем фильтр по тегу
    if (selectedTag !== 'Любой') {
      const tagWithHash = `#${selectedTag}`;
      result = result.filter(event => event.tag === tagWithHash);
    }
    
    // Применяем сортировку - всегда сортируем, убираем проверку на 'Любой'
    if (selectedSort === 'Сначала новые') {
      result.sort((a, b) => new Date(b.created_at).getTime() - new Date(a.created_at).getTime());
    } else if (selectedSort === 'Сначала старые') {
      result.sort((a, b) => new Date(a.created_at).getTime() - new Date(b.created_at).getTime());
    }
    
    filteredEvents = result;
  }

  async function loadEventsWithImages() {
    try {
      isLoading = true;
      error = null;
      
      // 1. Загружаем события
      const eventsResponse = await fetch('http://localhost:8000/events');
      
      if (!eventsResponse.ok) {
        throw new Error(`Ошибка при загрузке событий: ${eventsResponse.status}`);
      }
      
      const eventsData = await eventsResponse.json();
      
      // 2. Для каждого события определяем тег
      const eventsWithTags = eventsData.map((event: Event) => {
        const tag = getTagFromDescription(event.description);
        return {
          ...event,
          tag,
          image: getImageByTag(tag) // Устанавливаем запасное изображение по умолчанию
        };
      });
      
      // 3. Загружаем изображения для каждого события
      const eventsWithImages = await Promise.all(
        eventsWithTags.map(async (event: Event) => {
          const images = await loadEventImages(event.id);
          
          // Если есть изображения из галереи, используем первое как основное
          if (images && images.length > 0) {
            return {
              ...event,
              images,
              image: images[0].image_url
            };
          }
          
          return {
            ...event,
            images: []
          };
        })
      );
      
      events = eventsWithImages;
      
      // Применяем фильтры и сортировку
      applyFiltersAndSort();
      
    } catch (err) {
      console.error('Ошибка при загрузке событий:', err);
      error = err.message;
    } finally {
      isLoading = false;
    }
  }
  
  // Обработчики изменения фильтров
  function handleTagChange(event: Event) {
    selectedTag = event.target.value;
    applyFiltersAndSort();
  }
  
  function handleSortChange(event: Event) {
    selectedSort = event.target.value;
    applyFiltersAndSort();
  }
  
  // Переключение между изображениями события
  function handleImageClick(event: Event) {
    if (event.images && event.images.length > 1) {
      // Находим индекс текущего изображения
      const currentIndex = event.images.findIndex(img => img.image_url === event.image);
      
      // Переключаемся на следующее изображение или на первое, если это последнее
      const nextIndex = (currentIndex + 1) % event.images.length;
      event.image = event.images[nextIndex].image_url;
    }
  }
  
  onMount(() => {
    loadEventsWithImages();
  });
</script>

<div class="page-container">
  <div class="container">
    <header class="navbar">
      <div class="nav-buttons">
        <button class="nav-button">
          Расписание <span class="icon"><img src="/top1.svg" alt="Расписание" /></span>
        </button>
        <a href="/forum" class="nav-link">
          <button class="nav-button">
            Форум <span class="icon"><img src="/top2.svg" alt="Форум" /></span>
          </button>
        </a>
        <a href="/" class="nav-link">
          <button class="nav-button">
            Сервисы <span class="icon"><img src="/top3.svg" alt="Сервисы" /></span>
          </button>
        </a>
      </div>
    </header>

    <div class="profile">
      <div class="avatar"></div>
    </div>

    <main>
      <div class="content-header">
        <h2 class="main-title">Конференции<br>и мероприятия</h2>
        
        <div class="filters">
          <div class="filter-group">
            <label>Поиск по хештегам</label>
            <select class="filter-select" bind:value={selectedTag} on:change={handleTagChange}>
              <option>Любой</option>
              <option>Универсиада</option>
              <option>Университетская жизнь</option>
              <option>Конференция</option>
              <option>Олимпиада</option>
              <option>Мероприятие</option>
            </select>
          </div>
          
          <div class="filter-group">
            <label>По новизне</label>
            <select class="filter-select" bind:value={selectedSort} on:change={handleSortChange}>
              <option>Сначала новые</option>
              <option>Сначала старые</option>
            </select>
          </div>
        </div>
      </div>

      {#if isLoading}
        <div class="loading-state">
          <p>Загрузка событий...</p>
        </div>
      {:else if error}
        <div class="error-state">
          <p>Ошибка при загрузке данных: {error}</p>
          <button on:click={loadEventsWithImages} class="retry-button">Попробовать снова</button>
        </div>
      {:else if filteredEvents.length === 0}
        <div class="empty-state">
          <p>Нет событий, соответствующих выбранным фильтрам.</p>
          <button on:click={() => { selectedTag = 'Любой'; selectedSort = 'Сначала новые'; applyFiltersAndSort(); }} class="reset-filters-button">Сбросить фильтры</button>
        </div>
      {:else}
      <div class="events-list">
          {#each filteredEvents as event}
          <div class="event-card">
              <div class="event-image" on:click={() => handleImageClick(event)}>
              <img src={event.image} alt={event.title} />
                {#if event.images && event.images.length > 1}
                  <div class="image-indicator">
                    {#each event.images as _, i}
                      <span class={event.image === event.images[i].image_url ? 'active' : ''}></span>
                    {/each}
                  </div>
                {/if}
            </div>
            <div class="event-content">
              <div class="event-tag">{event.tag}</div>
              <h3 class="event-title">{event.title}</h3>
              <p class="event-description">{event.description}</p>
                <div class="event-details">
                  <div class="event-date">
                    <strong>Дата проведения:</strong> {formatDate(event.start_date)} - {formatDate(event.end_date)}
                  </div>
                  <div class="event-location">
                    <strong>Место:</strong> {event.location}
                  </div>
                  {#if event.price > 0}
                    <div class="event-price">
                      <strong>Стоимость:</strong> {event.price} ₽
                    </div>
                  {:else}
                    <div class="event-price free">
                      <strong>Участие бесплатное</strong>
                    </div>
                  {/if}
                </div>
              <button class="details-button">Подробнее</button>
            </div>
          </div>
        {/each}
      </div>
      {/if}
    </main>
  </div>
</div>

<style>
  @font-face {
    font-family: 'SF Pro Display';
    src: url('/font/SF-Pro-Display-Regular.otf') format('opentype');
    font-weight: 400;
    font-style: normal;
  }

  @font-face {
    font-family: 'SF Pro Display';
    src: url('/font/SF-Pro-Display-Medium.otf') format('opentype');
    font-weight: 500;
    font-style: normal;
  }

  @font-face {
    font-family: 'SF Pro Display';
    src: url('/font/SF-Pro-Display-Bold.otf') format('opentype');
    font-weight: 700;
    font-style: normal;
  }

  @font-face {
    font-family: 'SF Pro Display';
    src: url('/font/SF-Pro-Display-Light.otf') format('opentype');
    font-weight: 300;
    font-style: normal;
  }

  :global(body) {
    margin: 0;
    padding: 0;
    font-family: 'SF Pro Display', Arial, sans-serif;
    background-color: #ffffff;
  }

  .page-container {
    width: 100%;
    background-color: #ffffff;
    min-height: 100vh;
  }

  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
    position: relative;
  }

  /* Navbar */
  .navbar {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px 0;
  }

  .nav-buttons {
    display: flex;
    gap: 15px;
  }

  .nav-button {
    background-color: #f0f0f0;
    border: none;
    border-radius: 20px;
    padding: 8px 16px;
    font-size: 16px;
    display: flex;
    align-items: center;
    gap: 5px;
    cursor: pointer;
  }

  .icon {
    font-size: 18px;
    display: flex;
    align-items: center;
  }

  .icon img {
    width: 18px;
    height: 18px;
  }

  .nav-link {
    text-decoration: none;
  }

  /* Profile */
  .profile {
    position: fixed;
    top: 20px;
    right: 20px;
    z-index: 100;
  }

  .avatar {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background-color: #333;
  }

  /* Content Header */
  .content-header {
    margin: 40px 0;
  }

  .main-title {
    font-size: 36px;
    font-weight: 600;
    margin-bottom: 30px;
    line-height: 1.2;
  }

  /* Filters */
  .filters {
    display: flex;
    gap: 30px;
    margin-bottom: 30px;
  }

  .filter-group {
    display: flex;
    flex-direction: column;
    gap: 10px;
  }

  .filter-group label {
    font-size: 14px;
    color: #666;
  }

  .filter-select {
    padding: 10px 15px;
    border-radius: 12px;
    border: 1px solid #e0e0e0;
    background-color: #f5f5f5;
    width: 200px;
    font-family: 'SF Pro Display', Arial, sans-serif;
    font-size: 15px;
    appearance: none;
    background-image: url("data:image/svg+xml;charset=UTF-8,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='none' stroke='currentColor' stroke-width='2' stroke-linecap='round' stroke-linejoin='round'%3e%3cpolyline points='6 9 12 15 18 9'%3e%3c/polyline%3e%3c/svg%3e");
    background-repeat: no-repeat;
    background-position: right 10px center;
    background-size: 16px;
  }

  /* Events List */
  .events-list {
    display: flex;
    flex-direction: column;
    gap: 30px;
    margin-bottom: 60px;
  }

  .event-card {
    display: flex;
    background-color: #E4E4E4;
    border-radius: 20px;
    overflow: hidden;
  }

  .event-image {
    width: 270px;
    height: 270px;
    flex-shrink: 0;
    overflow: hidden;
    padding: 8px 0 8px 8px;
    display: flex;
    align-items: center;
    justify-content: center;
    box-sizing: border-box;
    position: relative;
    cursor: pointer;
  }

  .event-image img {
    width: 100%;
    height: 100%;
    object-fit: contain;
    max-width: 210px;
    max-height: 210px;
    transition: transform 0.3s ease;
  }

  .event-content {
    flex: 1;
    padding: 30px;
    position: relative;
    min-height: 210px;
    display: flex;
    flex-direction: column;
  }

  .event-tag {
    display: inline-block;
    background-color: #1A3882;
    color: white;
    padding: 5px 12px;
    border-radius: 15px;
    font-size: 12px;
    margin-bottom: 15px;
    align-self: flex-start;
  }

  .event-title {
    font-size: 24px;
    font-weight: 600;
    margin: 0 0 15px 0;
    line-height: 1.3;
  }

  .event-description {
    color: #444;
    line-height: 1.5;
    margin-bottom: 20px;
    flex-grow: 1;
  }

  .details-button {
    background-color: #1A3882;
    color: white;
    border: none;
    border-radius: 8px;
    padding: 10px 25px;
    font-size: 14px;
    font-weight: 500;
    cursor: pointer;
    align-self: flex-end;
    margin-top: auto;
  }

  .details-button:hover {
    background-color: #132a62;
  }

  @media (max-width: 768px) {
    .event-card {
      flex-direction: column;
    }

    .event-image {
      width: 100%;
      height: auto;
      aspect-ratio: 1/1;
      padding: 30px;
    }
    
    .event-image img {
      max-width: 100%;
      max-height: 100%;
    }
    
    .filters {
      flex-direction: column;
      gap: 15px;
    }
    
    .filter-select {
      width: 100%;
    }
    
    .event-content {
      padding: 20px;
    }
    
    .main-title {
      font-size: 28px;
    }
    
    .event-title {
      font-size: 20px;
    }
  }

  /* Новые стили */
  .loading-state,
  .error-state,
  .empty-state {
    text-align: center;
    padding: 50px 0;
    font-size: 18px;
    color: #666;
  }
  
  .error-state {
    color: #d32f2f;
  }
  
  .retry-button,
  .reset-filters-button {
    margin-top: 15px;
    padding: 8px 16px;
    background-color: #2F4A8D;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }
  
  .event-details {
    margin: 15px 0;
    font-size: 14px;
    color: #555;
    line-height: 1.5;
  }
  
  .event-price.free {
    color: #2e7d32;
  }

  /* Новые стили для галереи изображений */
  .image-indicator {
    position: absolute;
    bottom: 15px;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    gap: 5px;
    z-index: 10;
  }
  
  .image-indicator span {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background-color: rgba(255, 255, 255, 0.5);
  }
  
  .image-indicator span.active {
    background-color: #1A3882;
  }
  
  .event-image:hover img {
    transform: scale(1.05);
  }
</style> 