<script lang="ts">
  import { onMount } from 'svelte';
  
  interface MenuItem {
    id: number;
    title: string;
    image: string;
    description?: string;
    date?: string;
  }
  
  interface DayMenu {
    day: string;
    dayName: string;
    mainDish: string;
    calories: string;
    calories_details: string;
    items: {
      name: string;
      icon: string;
    }[];
  }
  
  // Хиты недели
  let weeklyHits: MenuItem[] = [
    {
      id: 1,
      title: 'ПРОТ',
      image: '/menu1.svg',
      description: 'ПРОТЕИНОВЫЙ БАТОНЧИК БЕЗ САХАРА СИНКАБАР'
    },
    {
      id: 2,
      title: 'SUSHI',
      image: '/menu2.svg',
      description: 'BORA BORA'
    },
    {
      id: 3,
      title: 'БЛИНЫ',
      image: '/menu3.svg',
      description: 'SO DELICIOUS!',
      date: '12-18 МАРТА'
    }
  ];
  
  // Дневное меню
  let daysMenu: DayMenu[] = [
    {
      day: 'Пн',
      dayName: 'Цезарь',
      mainDish: 'Цезарь',
      calories: '179.6 ккал',
      calories_details: 'Белки: 14.3 гр. Жиры: 8.6 гр. Углеводы: 10.8 гр.',
      items: [
        { name: 'Пицца', icon: '/menu/pizza_icon.png' },
        { name: 'Капучино', icon: '/menu/coffee_icon.png' },
        { name: 'Цезарь', icon: '/menu/cezar_icon.png' }
      ]
    },
    {
      day: 'Вт',
      dayName: 'Черный чай',
      mainDish: 'Черный чай',
      calories: 'Калорийность, 3 ккал, 1684 ккал ;',
      calories_details: 'Углеводы, 0.9 г, 219 г ; Углеводы (общие), 0.9 г',
      items: [
        { name: 'Чай', icon: '/menu/tea_icon.png' },
        { name: 'Рис', icon: '/menu/rice_icon.png' },
        { name: 'Том ям', icon: '/menu/tom_yum_icon.png' }
      ]
    }
  ];
  
  let currentHitIndex = 0;
  
  function prevHit() {
    if (currentHitIndex > 0) {
      currentHitIndex--;
    } else {
      currentHitIndex = weeklyHits.length - 1;
    }
  }
  
  function nextHit() {
    if (currentHitIndex < weeklyHits.length - 1) {
      currentHitIndex++;
    } else {
      currentHitIndex = 0;
    }
  }
  
  onMount(() => {
    // Автоматическое пролистывание карусели каждые 5 секунд
    const interval = setInterval(() => {
      nextHit();
    }, 5000);
    
    return () => {
      clearInterval(interval);
    };
  });
</script>

<div class="container">
  <!-- Навигационные кнопки -->
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

  <!-- Профиль -->
  <div class="profile">
    <div class="avatar"></div>
  </div>

  <h1 class="menu-title">Меню столовой</h1>

  <!-- Хиты недели -->
  <div class="hits-section">
    <h2 class="section-title">
      Хиты недели <span class="lightning-icon">⚡</span>
    </h2>
    
    <div class="hits-grid">
      {#each weeklyHits as hit}
        <div class="hit-card">
          <img src={hit.image} alt={hit.title} class="hit-image">
        </div>
      {/each}
    </div>
  </div>

  <!-- Дневное меню -->
  <div class="daily-menu">
    {#each daysMenu as day}
      <div class="day-card">
        <div class="day-header">
          <div class="day-icon">
            <span class="day-name">{day.day}</span>
          </div>
          <h3 class="dish-title">{day.dayName}</h3>
        </div>
        
        <div class="nutritional-info">
          <p>Калории: {day.calories}</p>
          <p class="details">{day.calories_details}</p>
        </div>
        
        <div class="dish-options">
          {#each day.items as item}
            <div class="dish-option">
              <img src={item.icon} alt={item.name} class="dish-icon">
              <span>{item.name}</span>
            </div>
          {/each}
        </div>
      </div>
    {/each}
  </div>
</div>

<style>
  /* Контейнер */
  .container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 20px;
    position: relative;
  }

  /* Навигация */
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

  .nav-button.active {
    background-color: #e0e0e0;
  }

  /* Профиль */
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
    cursor: pointer;
  }
  
  /* Основные стили для страницы меню */
  .menu-title {
    font-size: 32px;
    margin: 20px 0;
    color: #333;
    text-align: center;
  }
  
  /* Стили для раздела "Хиты недели" */
  .hits-section {
    margin: 30px 0;
  }
  
  .section-title {
    font-size: 24px;
    margin-bottom: 20px;
    display: flex;
    align-items: center;
    gap: 10px;
  }
  
  .lightning-icon {
    color: #FFD700;
    font-size: 20px;
  }
  
  /* Стили для грида хитов */
  .hits-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
    margin-bottom: 30px;
  }
  
  .hit-card {
    height: 300px;
    background-color: #f0f0f0;
    border-radius: 15px;
    overflow: hidden;
    position: relative;
  }
  
  .hit-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  
  /* Стили для дневного меню */
  .daily-menu {
    display: flex;
    flex-direction: column;
    gap: 20px;
    margin-bottom: 40px;
  }
  
  .day-card {
    background-color: #f8f8f8;
    border-radius: 15px;
    padding: 20px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  }
  
  .day-header {
    display: flex;
    align-items: center;
    margin-bottom: 15px;
    gap: 15px;
  }
  
  .day-icon {
    width: 50px;
    height: 50px;
    background-color: #333;
    border-radius: 10px;
    color: white;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    font-size: 20px;
  }
  
  .dish-title {
    font-size: 22px;
    margin: 0;
  }
  
  .nutritional-info {
    margin-bottom: 15px;
  }
  
  .nutritional-info p {
    margin: 5px 0;
    color: #666;
  }
  
  .details {
    font-size: 14px;
  }
  
  .dish-options {
    display: flex;
    justify-content: flex-end;
    gap: 20px;
  }
  
  .dish-option {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 5px;
  }
  
  .dish-icon {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    object-fit: cover;
  }
  
  /* Адаптивность */
  @media (max-width: 768px) {
    .hits-grid {
      grid-template-columns: 1fr;
    }
    
    .hit-card {
      height: 200px;
    }
    
    .dish-options {
      flex-wrap: wrap;
    }
  }
</style> 