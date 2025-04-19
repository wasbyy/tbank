<script>
  export let avatar = '/avatar.png';
</script>

<div class="profile">
  <div class="avatar" style="background-image: url({avatar})"></div>
</div>

<style>
  .profile {
    position: fixed;
    top: 40px;
    right: 40px;
    z-index: 100;
  }

  .avatar {
    width: 50px;
    height: 50px;
    border-radius: 50%;
    background-color: #ccc;
    background-size: cover;
    background-position: center;
    cursor: pointer;
  }
</style>