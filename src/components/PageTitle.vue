<template>
  <header class="relative">
  
  
  
            <nav class="second-nav" id="menusite">
    <div class="container">
        <div class="row">
            <div class="bg box-shadow">
            <div class="navbar navbar-default navbar-static-top" role="navigation">
<div class="navbar-header">
<button type="button" class="navbar-toggle" data-toggle="collapse" data-target="#menu-site-default">
    <span class="sr-only">&nbsp;</span> <span class="icon-bar">&nbsp;</span> <span class="icon-bar">&nbsp;</span> <span class="icon-bar">&nbsp;</span>
</button>
</div>
<div class="collapse navbar-collapse" id="menu-site-default">
<ul class="nav navbar-nav">
    <li><a class="home" href="/" title="Trang nhất"><em class="fa fa-lg fa-home">&nbsp;</em><span class="visible-xs-inline-block"> Trang nhất</span></a></li>
                <li rol="presentation"><a class="dropdown-toggle" href="/tin-giao-duc/" role="button" aria-expanded="false" title="TIN GIÁO DỤC">  TIN GIÁO DỤC</a> </li>
    <li rol="presentation"><a class="dropdown-toggle" href="/tuyen-sinh/" role="button" aria-expanded="false" title="TUYỂN SINH">  TUYỂN SINH</a> </li>
    <li rol="presentation"><a class="dropdown-toggle" href="/huong-nghiep/" role="button" aria-expanded="false" title="HƯỚNG NGHIỆP">  HƯỚNG NGHIỆP</a> </li>
    <li rol="presentation"><a class="dropdown-toggle" href="/thu-vien-nghe/" role="button" aria-expanded="false" title="THƯ VIỆN NGHỀ">  THƯ VIỆN NGHỀ</a> </li>
    <li rol="presentation"><a class="dropdown-toggle" href="/cong-nghe/" role="button" aria-expanded="false" title="CÔNG NGHỆ">  CÔNG NGHỆ</a> </li>
    <li rol="presentation"><a class="dropdown-toggle" href="/giai-tri/" role="button" aria-expanded="false" title="GIẢI TRÍ">  GIẢI TRÍ</a> </li>
    <li rol="presentation"><a class="dropdown-toggle" href="/goc-chia-se/" role="button" aria-expanded="false" title="GÓC CHIA SẺ">  GÓC CHIA SẺ</a> </li>
    <li rol="presentation"><a class="dropdown-toggle" href="/thoi-su/" role="button" aria-expanded="false" title="SỨC KHỎE">  SỨC KHỎE</a> </li>
</ul>
</div>
</div>
            </div>
        </div>
    </div>
</nav>
<center><img src="/images/hpny.jpg" /></center>





    <!-- hero image slot -->
    <slot name="image"></slot>
    <!-- title block -->
    <div class="frame frame--header relative" :class="headerLayoutStyle">
      <nav
        class="frame-area-a Heading Heading-4xl font-medium fixed z-50 Logo"
        :class="[headingInvertStyle, scrollInvertStyle]"
      >
        <!-- v-smooth-scroll="{ duration: 1000 }" -->
        <a v-if="$route.path === '/'" href="#top">
          Linh
        </a>
        <saber-link v-else to="/">
          <!-- &#8592; -->
          Linh
        </saber-link>
      </nav>
      <div class="frame-area-b">
        <h1 class="Heading Heading-4xl font-medium" :class="headingInvertStyle">
          {{ page.title }}
        </h1>
        <PageTitleMeta
          v-if="showMeta"
          :page="page"
          :invert="invert"
          :class="[textInvertStyle, { 'opacity-75': invert }]"
          class="Space-sm-t"
        ></PageTitleMeta>
        <p v-if="page.lede" class="Text-xl Block-xs-t" :class="textInvertStyle">
          {{ page.lede }}
          
          

          
          
          
          
          
          
          
          
          
          
          
          
          
          
          
          <template v-if="$route.path === '/'"> 
            <saber-link to="https://cytimy.com" class="Link text-brand-red">
    <img src="https://github.com/Van-may/img/raw/main/thuylinh_error.png" alt="Shop của Sago" />
  </saber-link>
          </template>
        </p>
        <!-- default slot -->
        <slot></slot>
      </div>
      <!-- intersection-observer target -->
      <div ref="observe" class="io-target"></div>
    </div>
  </header>
</template>

<script>
// import Vue from "vue";
import PageTitleMeta from "../components/PageTitleMeta";
// import vueSmoothScroll from "vue-smooth-scroll";
// Vue.use(vueSmoothScroll);

export default {
  components: {
    PageTitleMeta,
  },
  props: {
    page: Object,
    invert: {
      type: Boolean,
      default: false,
    },
    showMeta: {
      type: Boolean,
      default: false,
    },
  },
  data: () => ({
    visible: false,
  }),
  computed: {
    headerLayoutStyle() {
      if (this.$route.path === "/about") {
        return "Block-t Block-sm-b";
      }
      return "Block";
    },
    headingInvertStyle() {
      return this.invert && "text-white";
    },
    scrollInvertStyle() {
      return this.$route.path !== "/about" && !this.visible && "text-black-important";
    },
    textInvertStyle() {
      return this.invert ? "text-white" : "text-gray-dark";
      /* if (this.$route.path === "/about") {
        return "text-white";
      } else if (this.invert) {
        return "text-white opacity-100";
      }
      return "text-gray-dark"; */
    },
  },
  mounted() {
    if (this.$route.path !== "/" || this.$route.path !== "/about") {
      // use i-o to toggle CFd logo in <PageTitle> when it leaves the viewport
      // https://www.notion.so/callum/Intersection-observer-use-in-Vue-ff50d8e8e79647b7bccfbe861b2eaf5b
      const io = new IntersectionObserver(entries => {
        // Log available data when an intersection happens
        // console.log(entries);
        // Element enters the viewport
        if (entries[0].intersectionRatio !== 0) {
          this.visible = true;
          // Element leaves the viewport
        } else {
          this.visible = false;
        }
      });

      // Elements to be observed
      const box = this.$refs.observe;

      // Start observing box
      io.observe(box);
    }
  },
};
</script>

<style lang="postcss">
@screen mobile {
  .Logo {
    @apply relative;
    margin-top: calc(-1.333 * var(--spacing8));
  }
}
/* IO thing */
.io-target {
  @apply absolute;
  bottom: 9vh;
  /* height: 2px;
  width: 2px;
  background-color: salmon; */
}
.text-black-important {
  @apply text-black !important;
  /* filter: invert(1); */
}
/* .Logo {
  background-clip: text;
  color: transparent;
  filter: invert(1) grayscale(1) contrast(9);
} */




































.row {
    margin-left: -5px;
    margin-right: -5px;
}
.second-nav .bg {
    background: #cccccc;
    background-image: linear-gradient(to bottom,rgba(0,0,0,0.05) 0%,rgba(0,0,0,0) 100%) !important;
    -webkit-border-top-left-radius: 5px;
    -webkit-border-top-right-radius: 5px;
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
}

.box-shadow {
    box-shadow: 0 0 4px rgba(0,0,0,0.15);
    -webkit-box-shadow: 0 0 4px rgba(0,0,0,0.15);
}

#menusite .navbar-default {
    background-color: #428BCA;
    border-bottom-color: #428BCA;
    border-bottom-width: 1px;
    border-bottom-style: solid;
    -webkit-border-top-left-radius: 5px;
    -webkit-border-top-right-radius: 5px;
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
}

.navbar {
    min-height: 35px;
}

.navbar-default {
    background-color: #33004B !important;
}

.navbar-default {
    background-color: #0855a1;
    border-color: #064481;
}

.navbar-static-top {
    z-index: 1000;
    border-width: 0 0 1px;
}

.navbar {
    position: relative;
    min-height: 50px;
    margin-bottom: 0;
    border: 1px solid transparent;
}

.navbar-header {
    float: left;
}

.navbar-default .navbar-collapse, .navbar-default .navbar-form {
    border-color: #064481;
}

.nav {
    height: 35px;
}

.navbar-nav {
    float: left;
    margin: 0;
}

.navbar-nav {
    margin: 8px -5px;
}

.nav {
    margin-bottom: 0;
    padding-left: 0;
    list-style: none;
}

#menusite .navbar-default .navbar-nav > li:first-child {
    margin-left: 4px;
}
#menusite .navbar-default .navbar-nav > li {
    margin-left: 1px;
}
.navbar-nav > li {
    float: left;
}
.nav > li {
    position: relative;
    display: block;
}

#menusite .navbar-default .navbar-nav > li > a {
    color: #fff !important;
    font-weight: bold;
    font-size: 13px;
    line-height: 12px;
}
#menusite .navbar-default .navbar-nav > li > a {
    color: #fff !important;
}
#menusite .navbar-nav > li > a {
    white-space: nowrap;
}
.navbar-default .navbar-nav > li > a {
    color: #999999;
}
.navbar-nav > li > a {
    padding: 12px;
}
.navbar-nav > li > a {
    padding-top: 12px;
    padding-bottom: 16px;
}
.navbar-nav > li > a {
    padding: 15px;
}
.navbar-nav > li > a {
    padding-top: 10px;
    padding-bottom: 10px;
    line-height: 18px;
}
.nav > li > a {
    position: relative;
    display: block;
    padding: 10px 15px;
}
a, a:link, a:active, a:visited {
    color: #1a3f5e;
}
#menusite .navbar-default .navbar-nav > li > a:hover, #menusite .navbar-default .navbar-nav > li > a:focus, #menusite .navbar-default .navbar-nav > .active > a, #menusite .navbar-default .navbar-nav > .active > a:hover, #menusite .navbar-default .navbar-nav > .active > a:focus, #menusite .navbar-default .navbar-nav > .open > a, #menusite .navbar-default .navbar-nav > .open > a:hover, #menusite .navbar-default .navbar-nav > .open > a:focus {
    background: none !important;
    color: #f00 !important;
}
a {
    color: #428bca;
    text-decoration: none;
}
a {
    background-color: transparent;
}









</style>
