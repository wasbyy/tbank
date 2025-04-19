<script>
  export let avatar = '/avatar.png';
</script>

<div class="profile">
  <div class="avatar"></div>
</div>

<style>
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
    cursor: pointer;
  }
</style> 