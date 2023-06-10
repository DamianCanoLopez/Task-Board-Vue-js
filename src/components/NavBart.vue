<script>
    export default {
        name: 'NavBart',
    }
</script>

<template>
    <div id="nav">
        <img src='../assets/img/logoP.svg' alt="logo">
        <span class="navbar-text">
            <div class="social-icon">
                <a href="https://www.linkedin.com/in/carlos-damian-cano-lopez-399812260/" style='textDecoration: none color: white' target="_blank"><img src="../assets/img/nav-icon1.svg" alt="Icon"/></a>
                <a href="https://github.com/DamianCanoLopez" style='textDecoration: none color: white' target="_blank"><img src="../assets/img/nav-icon4.svg"/></a>
                <a href="https://damiancanolopez.vercel.app/" style='textDecoration: none color: white' target="_blank"><img src="../assets/img/nav-icon5.svg" alt="Icon"/></a>
            </div>
        </span>
    </div>
</template>

<style>
#nav {
  background-color: black;
  width: 100%;
  display: flex;
  justify-content: space-between;
  padding: 3%;
}

span.navbar-text {
  display: flex;
  align-items: center;
}

.social-icon {
  display: flex;
  align-items: center;
  margin-left: 14px;
}

.social-icon a {
  width: 42px;
  height: 42px;
  background: rgba(217, 217, 217, 0.1);
  display: flex;
  border-radius: 50%;
  margin-right: 6px;
  align-items: center;
  justify-content: center;
  line-height: 1;
  border: 1px solid rgba(255, 255, 255, 0.5);
  position: relative;
  overflow: hidden;
  transition: 0.3s ease-in-out;
}

.social-icon a::before {
  content: '';
  width: 100%;
  height: 100%;
  position: absolute;
  background-color: #ffffff;
  border-radius: 50%;
  transform: scale(0);
  transition: 0.3s ease-in-out;
}

.social-icon a:hover::before {
  transform: scale(1);
}

.social-icon a img {
  width: 40%;
  z-index: 1;
  transition: 0.3s ease-in-out;
}

.social-icon a:hover img {
  filter: brightness(0) saturate(100%) invert(0%) sepia(7%) saturate(98%) hue-rotate(346deg) brightness(95%) contrast(86%);
}

/* Estilos para pantallas pequeñas */
@media screen and (max-width: 768px) {
  #nav {
    flex-direction: column;
    align-items: center;
    padding: 3% 0;
  }

  .social-icon {
    margin-top: 10px;
  }
}

/* Estilos para pantallas de 769px a 1024px */
@media screen and (min-width: 769px) and (max-width: 1024px) {
  #nav {
    flex-direction: column;
    align-items: center;
    padding: 3% 0;
  }
}

</style>