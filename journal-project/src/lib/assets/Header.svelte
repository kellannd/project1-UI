<link
  rel="stylesheet"
  href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.3/font/bootstrap-icons.min.css"
/>
<script>

    let isUserInfoHidden = true;

    function hoverUserInfo() {
    isUserInfoHidden = !isUserInfoHidden;
  }
</script>
<main>
  <div class="header">
    <a on:mouseenter={ hoverUserInfo } on:mouseleave={hoverUserInfo}><i class="bi bi-person-circle"></i></a>
    <div class="userInfo" hidden = { isUserInfoHidden }>
      <p>User: User</p>
      <p>Joined: January 1, 2023</p>
    </div>
  </div>
</main>

<style>
.userInfo {
    background-color: white;
    color: black;
    width: 300px;
    position: absolute;
    right: 0;
    top: 0;
    margin-top: 70px;
    text-align: center;
    font-size: 20px;
    padding: 20px;
    box-shadow: 0 0 3px black;
}
  .header {
    background-color: #443B3D;
    color: #f1f1f1;
    height: 80px;
    position: relative;
  }

  a {
    color: white;
  }

  .bi-person-circle {
    color: white;
    font-size: 40px;
    position: absolute;
    right: 0;
    top: 0;
    padding-top: 20px;
    padding-right: 20px;
  }
</style>
