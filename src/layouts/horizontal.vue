<script>
import HorizontalTopbar from "@/components/horizontal-topbar";
// import HorizontalNav from "@/components/horizontal-nav";
import Sidebar from "../components/side-bar.vue";
import RightBar from "@/components/right-bar";
import Footer from "@/components/footer";

import { useLayoutStore } from "@/state/pinia";
const layoutStore = useLayoutStore();

/**
 * Horizontal-layout
 */
export default {
  props: {},
  components: {
    HorizontalTopbar,
    // HorizontalNav,
    Sidebar,
    Footer,
    RightBar
  },
  computed: {
    layoutWidth() {
      return layoutStore.layoutWidth;
    },
    topbar() {
      return layoutStore.topbar;
    },
    loader() {
      return layoutStore.loader;
    },
    mode(){
      return layoutStore.mode
    }

  },
  created: () => {
    document.body.setAttribute("data-layout", "horizontal");
    document.body.setAttribute("data-topbar", "dark");
    document.body.removeAttribute("data-sidebar");
    document.body.removeAttribute("data-layout-size");
    document.body.classList.remove("auth-body-bg");
  },
  methods: {
    toggleRightSidebar() {
      document.body.classList.toggle("right-bar-enabled");
    },
    hideRightSidebar() {
      document.body.classList.remove("right-bar-enabled");
    }
  },
  mounted() {
    if (this.loader === true) {
      document.getElementById("preloader").style.display = "block";
      document.getElementById("status").style.display = "block";

      setTimeout(function () {
        document.getElementById("preloader").style.display = "none";
        document.getElementById("status").style.display = "none";
      }, 2500);
    } else {
      document.getElementById("preloader").style.display = "none";
      document.getElementById("status").style.display = "none";
    }
  }
};
</script>

<template>
  <div>
    <div id="preloader">
      <div id="status">
        <div class="spinner-chase">
          <div class="chase-dot"></div>
          <div class="chase-dot"></div>
          <div class="chase-dot"></div>
          <div class="chase-dot"></div>
          <div class="chase-dot"></div>
          <div class="chase-dot"></div>
        </div>
      </div>
    </div>
    <!-- Begin page -->
    <div id="layout-wrapper">
      <HorizontalTopbar :type="topbar" :width="layoutWidth"  :mode="mode"/>
      <!-- <HorizontalNav /> -->
      <!-- ============================================================== -->
      <!-- Start right Content here -->
      <!-- ============================================================== -->
      <div class="main-content">
        <Sidebar/>
        <div class="page-content">
          <BContainer fluid>
            <slot />
          </BContainer>
          <!-- container-fluid -->
        </div>
        <!-- End Page-content -->
        <Footer />
      </div>
      <!-- end main content-->
    </div>
    <!-- END layout-wrapper -->
    <RightBar />
  </div>
</template>

<style scoped>
/* Main Layout Styles */
.layout-content {
  display: flex;
}

.page-content {
  flex: 1;
  margin-left: 250px; /* Match sidebar width */
  transition: margin-left 0.3s ease;
}

.content-expanded {
  margin-left: 0;
}

/* Media Queries */
@media (max-width: 768px) {
  .page-content {
    margin-left: 0;
  }
  .sidebar {
    transform: translateX(-100%);
  }
  .sidebar-hidden {
    transform: translateX(-100%);
  }
}
</style>