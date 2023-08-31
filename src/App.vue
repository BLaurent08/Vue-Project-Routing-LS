<script>
export default {
  name: 'App',
  data() {
    return {
      title: 'Vue 3 Tutorial',
    }
  },
  methods: {
    updateTitle(route) {
      this.title = route.meta.title || 'Home';
    }
  },
  mounted() {
    this.updateTitle(this.$route);
  },
  watch: {
    $route(to, from) {
      this.updateTitle(to);
    }
  }
}

document.addEventListener('click', function(event) {
  var navbarCollapse = document.querySelector('.navbar-collapse');
  var targetElement = event.target;

  // Check if the clicked element is outside the navbar-collapse
  if (!navbarCollapse.contains(targetElement)) {
    // Toggle the visibility of the navbar-collapse
    navbarCollapse.classList.remove('show');
  }
});

var links = document.querySelectorAll('.navbar-collapse a');

links.forEach(function(link) {
  link.addEventListener('click', function() {
    var navbarCollapse = document.querySelector('.navbar-collapse');
    navbarCollapse.classList.remove('show');
  });
});
</script>

<template>
  <header class="mx-0 p-0 mb-2">
    <nav class="navbar-expand-lg bg-opaque pb-5" :class="['navbar', {'taller': title !== 'Home'}]" data-bs-theme='dark'>
      <div class="container-fluid">
        <RouterLink class="navbar-brand popper-text-dark fs-1 fw-bold text-white mb-0 pb-0 popper-link" to="/">Tutorials
          Co.<span class="fs-3 ps-2 fw-semibold">{{ title }}</span></RouterLink>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup"
          aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon popper-dark"></span>
        </button>
        <div class="collapse navbar-collapse bg-opaque" id="navbarNavAltMarkup">
          <div class="navbar-nav gap-sm-4 ps-3">
            <RouterLink class="nav-link fs-4 popper-text-dark fw-semibold text-white popper-link rounded-4" to="/">Home
            </RouterLink>
            <RouterLink class="nav-link fs-4 popper-text-dark fw-semibold text-white popper-link rounded-4" to="/add">Add
            </RouterLink>
            <RouterLink class="nav-link fs-4 popper-text-dark fw-semibold text-white popper-link rounded-4"
              to="/tutorial">Tutorials
            </RouterLink>
          </div>
        </div>
      </div>
    </nav>
  </header>
  <main>
    <div class="row mx-0 p-0">
      <div class="col-sm-4 box rounded-5 mx-0 p-4">
        <div class="row p-sm-4 mx-0 align-middle justify-content-center gap-4">
          <RouterView />
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
.bg-opaque {
  background-color: rgba(18, 39, 20, 0.3);
  /* blurs the background */
  backdrop-filter: blur(.2rem);
  z-index: 1000;
}

.navbar-collapse {
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0), rgba(0, 0, 0, 1)) !important;
  z-index: 1000;
  border-radius: 1rem;
}

.box {
  position: absolute;
  top: 7rem;
  left: 50%;
  width: 40rem;
  transform: translate(-50%);
  background-color: rgba(50, 50, 50, 0.15);
  /* blurs the background */
  backdrop-filter: blur(.5rem);
}

.taller {
  height: 6.5rem;
}

.navbar {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  min-height: 5rem;
  max-height: 6.5rem;
  height: auto;
}

@media (max-width: 600px) {
  .box {
    position: absolute;
    top: 9rem;
    left: 50%;
    width: 40rem;
    transform: translate(-50%);
    background-color: rgba(50, 50, 50, 0.15);
    backdrop-filter: blur(.5rem);
  }
}
</style>
