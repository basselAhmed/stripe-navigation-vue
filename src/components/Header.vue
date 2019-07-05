<template>
  <header class="cd-morph-dropdown" ref="element">
    <a href="#0" class="nav-trigger" ref="mobileTrigger">
      Open Nav
      <span aria-hidden="true"></span>
    </a>
    <nav class="main-nav" ref="mainNav">
      <ul>
        <li class="has-dropdown gallery" data-content="about">
          <a href="#0">About</a>
        </li>
        <li class="has-dropdown links" data-content="pricing">
          <a href="#0">Pricing</a>
        </li>
        <li class="has-dropdown button" data-content="contact">
          <a href="#0">Contact</a>
        </li>
      </ul>
    </nav>
    <div class="morph-dropdown-wrapper" ref="morphWrapper">
      <div class="dropdown-list" ref="dropdownList">
        <ul>
          <li id="about" class="dropdown gallery">
            <a href="#0" class="label">About</a>
            <div class="content">
              <ul>
                <li>
                  <a href="#0" @click="hideAll">
                    <em>Title here</em>
                    <span>A brief description here</span>
                  </a>
                </li>
                <li>
                  <a href="#0" @click="hideAll">
                    <em>Title here</em>
                    <span>A brief description here</span>
                  </a>
                </li>
                <li>
                  <a href="#0" @click="hideAll">
                    <em>Title here</em>
                    <span>A brief description here</span>
                  </a>
                </li>
                <li>
                  <a href="#0" @click="hideAll">
                    <em>Title here</em>
                    <span>A brief description here</span>
                  </a>
                </li>
              </ul>
            </div>
          </li>
          <li id="pricing" class="dropdown links">
            <a href="#0" class="label">Pricing</a>
            <div class="content">
              <ul>
                <li>
                  <h2>Services</h2>
                  <ul class="links-list">
                    <li>
                      <a href="#0" @click="hideAll">Logo Design</a>
                    </li>
                    <li>
                      <a href="#0" @click="hideAll">Branding</a>
                    </li>
                    <li>
                      <a href="#0" @click="hideAll">Web Design</a>
                    </li>
                    <li>
                      <a href="#0" @click="hideAll">iOS</a>
                    </li>
                    <li>
                      <a href="#0" @click="hideAll">Android</a>
                    </li>
                    <li>
                      <a href="#0" @click="hideAll">HTML/CSS/JS</a>
                    </li>
                    <li>
                      <a href="#0" @click="hideAll">Packaging</a>
                    </li>
                    <li>
                      <a href="#0" @click="hideAll">Mobile</a>
                    </li>
                    <li>
                      <a href="#0" @click="hideAll">UI/UX</a>
                    </li>
                    <li>
                      <a href="#0" @click="hideAll">Prototyping</a>
                    </li>
                  </ul>
                </li>
                <li>
                  <h2>Projects</h2>
                  <ul class="links-list">
                    <li>
                      <a href="#0" @click="hideAll">Logo Design</a>
                    </li>
                    <li>
                      <a href="#0" @click="hideAll">Branding</a>
                    </li>
                    <li>
                      <a href="#0" @click="hideAll">Web Design</a>
                    </li>
                    <li>
                      <a href="#0" @click="hideAll">iOS</a>
                    </li>
                    <li>
                      <a href="#0" @click="hideAll">Android</a>
                    </li>
                    <li>
                      <a href="#0" @click="hideAll">HTML/CSS/JS</a>
                    </li>
                  </ul>
                </li>
              </ul>
            </div>
          </li>
          <li id="contact" class="dropdown button">
            <a href="#0" class="label">Contact</a>
            <div class="content">
              <ul class="links-list">
                <li>
                  <a href="#0" @click="hideAll">Link #1</a>
                </li>
                <li>
                  <a href="#0" @click="hideAll">Link #2</a>
                </li>
                <li>
                  <a href="#0" @click="hideAll">Link #3</a>
                </li>
                <li>
                  <a href="#0" @click="hideAll">Link #4</a>
                </li>
                <li>
                  <a href="#0" @click="hideAll">Link #5</a>
                </li>
                <li>
                  <a href="#0" @click="hideAll">Link #6</a>
                </li>
              </ul>
              <a href="#0" @click="hideAll" class="btn">Get in Touch</a>
            </div>
          </li>
          <div class="bg-layer" aria-hidden="true" ref="dropdownBG"></div>
        </ul>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",
  mounted() {
    this.init();
  },
  methods: {
    init() {
      const mainNavigationItems = this.$refs.mainNav.querySelectorAll(
        ".has-dropdown"
      );
      mainNavigationItems.forEach(item => {
        item.addEventListener("mouseenter", () => {
          this.showDropdown(item);
        });
        item.addEventListener("mouseleave", () => {
          if (
            this.$refs.mainNav.querySelectorAll(".has-dropdown:hover")
              .length === 0 &&
            this.$refs.morphWrapper.querySelectorAll(".dropdown-list:hover")
              .length === 0
          )
            this.hideDropdown(item);
        });
      });

      this.$refs.element.addEventListener("mouseleave", () => {
        const activeItems = this.$refs.morphWrapper.querySelectorAll(".active");
        activeItems.forEach(item => item.classList.remove("active"));
        this.$refs.element.classList.remove("is-dropdown-visible");
      });

      this.$refs.mobileTrigger.addEventListener("click", () => {
        this.reset();
        if (this.$refs.element.classList.contains("nav-open")) {
          this.$refs.element.classList.remove("nav-open");
        } else {
          this.$refs.element.classList.add("nav-open");
        }
      });
    },
    showDropdown(item) {
      const selectedDropdown = this.$refs.dropdownList.querySelector(
        `#${item.dataset.content}`
      );
      const selectedDropdownHeight = selectedDropdown.clientHeight;
      const content = [...selectedDropdown.childNodes].find(item =>
        item.classList.contains("content")
      );
      const selectedDropdownWidth = content.clientWidth;
      const selectedDropdownLeft =
        item.offsetLeft + item.clientWidth / 2 - selectedDropdownWidth / 2;

      this.updateDropdown(
        selectedDropdown,
        parseInt(selectedDropdownHeight),
        selectedDropdownWidth,
        parseInt(selectedDropdownLeft)
      );
      const activeDropdownItems = this.$refs.morphWrapper.querySelectorAll(
        ".active"
      );
      activeDropdownItems.forEach(item => item.classList.remove("active"));
      const activeNavItems = this.$refs.mainNav.querySelectorAll(".active");
      activeNavItems.forEach(item => item.classList.remove("active"));
      item.classList.add("active");
      const children = [...selectedDropdown.parentNode.children];
      const prev = children.filter(
        (el, index) => index < children.indexOf(selectedDropdown)
      );
      const after = children.filter(
        (el, index) => index > children.indexOf(selectedDropdown)
      );
      selectedDropdown.classList.add("active");
      selectedDropdown.classList.remove("move-left");
      selectedDropdown.classList.remove("move-right");
      if (prev.length > 0) {
        prev.forEach(el => {
          el.classList.add("move-left");
        });
      }
      if (after.length > 0) {
        after.forEach(el => {
          el.classList.add("move-right");
        });
      }
      this.$refs.element.classList.add("is-dropdown-visible");
    },
    hideDropdown(item) {
      const selectedDropdown = this.$refs.dropdownList.querySelector(
        `#${item.dataset.content}`
      );
      const prevs = this.$refs.dropdownList.querySelectorAll(".move-left");
      const afters = this.$refs.dropdownList.querySelectorAll(".move-right");
      prevs.forEach(el => {
        el.classList.remove("move-left");
      });
      afters.forEach(el => {
        el.classList.remove("move-right");
      });
      selectedDropdown.classList.remove("active");
      item.classList.remove("active");
      this.$refs.element.classList.remove("is-dropdown-visible");
    },
    updateDropdown(dropdownItem, height, width, left) {
      this.$refs.dropdownList.style["transform"] = `translateX(${left}px)`;
      this.$refs.dropdownList.style["width"] = `${width}px`;
      this.$refs.dropdownList.style["height"] = `${height}px`;

      // this.$refs.dropdownBG.style[
      //   "transform"
      // ] = `scaleX(${width}) scaleY(${height})`;
    },
    reset() {
      this.$refs.dropdownList.style["transform"] = "";
      this.$refs.dropdownList.style["width"] = "";
      this.$refs.dropdownList.style["height"] = "";
      // this.$refs.dropdownBG.style["transform"] = "";
      const activeDropdownItems = this.$refs.morphWrapper.querySelectorAll(
        ".active"
      );
      activeDropdownItems.forEach(item => item.classList.remove("active"));
      const activeNavItems = this.$refs.mainNav.querySelectorAll(".active");
      activeNavItems.forEach(item => item.classList.remove("active"));
      this.$refs.element.classList.remove("is-dropdown-visible");
    },
    hideAll() {
      this.$refs.element
        .querySelectorAll(".active")
        .forEach(el => el.classList.remove("active"));
      this.$refs.element.classList.remove("is-dropdown-visible");
    }
  }
};
</script>

<style scoped lang="stylus">
.cd-morph-dropdown
  position relative
  height 60px
  background-color #fff

.cd-morph-dropdown::before
  content 'mobile'
  display none

.cd-morph-dropdown .nav-trigger
  position absolute
  top 0
  right 0
  height 60px
  width 60px
  overflow hidden
  text-indent 100%
  white-space nowrap
  color transparent

.cd-morph-dropdown .nav-trigger span, .cd-morph-dropdown .nav-trigger span::after, .cd-morph-dropdown .nav-trigger span::before
  position absolute
  background-color #1a1a1a
  height 3px
  width 26px

.cd-morph-dropdown .nav-trigger span
  left 50%
  top 50%
  bottom auto
  right auto
  -webkit-transform translateX(-50%) translateY(-50%)
  -ms-transform translateX(-50%) translateY(-50%)
  transform translateX(-50%) translateY(-50%)
  -webkit-transition background-color 0.3s
  transition background-color 0.3s

.cd-morph-dropdown .nav-trigger span::after, .cd-morph-dropdown .nav-trigger span::before
  content ''
  left 0
  -webkit-transition -webkit-transform 0.3s
  transition -webkit-transform 0.3s
  transition transform 0.3s
  transition transform 0.3s, -webkit-transform 0.3s

.cd-morph-dropdown .nav-trigger span::before
  -webkit-transform translateY(-9px)
  -ms-transform translateY(-9px)
  transform translateY(-9px)

.cd-morph-dropdown .nav-trigger span::after
  -webkit-transform translateY(9px)
  -ms-transform translateY(9px)
  transform translateY(9px)

.cd-morph-dropdown.nav-open .nav-trigger span
  background-color transparent

.cd-morph-dropdown.nav-open .nav-trigger span::before
  -webkit-transform rotate(45deg)
  -ms-transform rotate(45deg)
  transform rotate(45deg)

.cd-morph-dropdown.nav-open .nav-trigger span::after
  -webkit-transform rotate(-45deg)
  -ms-transform rotate(-45deg)
  transform rotate(-45deg)

.cd-morph-dropdown .main-nav
  display none

.cd-morph-dropdown .morph-dropdown-wrapper
  display none
  position absolute
  top 60px
  left 0
  width 100%
  padding 1.2em 5%
  box-shadow inset 0 1px 0 #e6e6e6
  background-color #fff

.cd-morph-dropdown.nav-open .morph-dropdown-wrapper
  display block

.cd-morph-dropdown .dropdown-list>ul>li
  margin-bottom 3.3em

.cd-morph-dropdown .label
  display block
  font-size 2.2rem
  color #1a1a1a
  margin-bottom 0.8em

.cd-morph-dropdown .content li::after
  clear both
  content ''
  display block

.cd-morph-dropdown .gallery .content li
  margin-bottom 1.4em

.cd-morph-dropdown .gallery .content a
  display block

.cd-morph-dropdown .gallery .content a::before
  content ''
  display inline-block
  float left
  height 54px
  width 54px
  margin-right 0.6em
  background red
  border-radius 50%
  -webkit-transition background 0.2s
  transition background 0.2s

.cd-morph-dropdown .gallery .content a span, .cd-morph-dropdown .gallery .content a em
  display block
  line-height 1.2

.cd-morph-dropdown .gallery .content a em
  font-size 1.8rem
  padding 0.4em 0 0.2em
  color #1a1a1a

.cd-morph-dropdown .gallery .content a span
  font-size 1.4rem
  color #a6a6a6

.cd-morph-dropdown .gallery .content a:hover::before
  background-color #1a1a1a

// .cd-morph-dropdown .gallery li:nth-of-type(1) a::before {
// background: #f4e58a url('../img/cd-gallery-icons.svg') no-repeat 0 0;
// }

// .cd-morph-dropdown .gallery li:nth-of-type(2) a::before {
// background: #f4af6d url('../img/cd-gallery-icons.svg') no-repeat -54px 0;
// }

// .cd-morph-dropdown .gallery li:nth-of-type(3) a::before {
// background: #db6356 url('../img/cd-gallery-icons.svg') no-repeat -108px 0;
// }

// .cd-morph-dropdown .gallery li:nth-of-type(4) a::before {
// background: #8d4645 url('../img/cd-gallery-icons.svg') no-repeat -162px 0;
// }
.cd-morph-dropdown .links .content>ul>li
  margin-top 1em

.cd-morph-dropdown .links-list a, .cd-morph-dropdown .btn
  display block
  margin-left 14px
  font-size 2.2rem
  line-height 1.6

.cd-morph-dropdown .links-list a:hover, .cd-morph-dropdown .btn:hover
  color #1a1a1a

.cd-morph-dropdown .content h2
  color #a6a6a6
  text-transform uppercase
  font-weight 700
  font-size 1.3rem
  margin 20px 0 10px 14px

@media only screen and (min-width: 1000px)
  .cd-morph-dropdown
    position absolute
    height 80px
    left 0
    top 0
    width 100%
    padding 0
    text-align center
    background-color transparent

  .cd-morph-dropdown::before
    content 'desktop'

  .cd-morph-dropdown .nav-trigger
    display none

  .cd-morph-dropdown .main-nav
    display inline-block

  .cd-morph-dropdown .main-nav>ul>li
    display inline-block
    float left

  .cd-morph-dropdown .main-nav>ul>li>a
    display block
    padding 0 1.8em
    height 70px
    line-height 70px
    color #fff
    font-size 1.8rem
    -webkit-font-smoothing antialiased
    -moz-osx-font-smoothing grayscale
    -webkit-transition opacity 0.2s
    transition opacity 0.2s

  .cd-morph-dropdown.is-dropdown-visible .main-nav>ul>li>a
    opacity 0.6

  .cd-morph-dropdown.is-dropdown-visible .main-nav>ul>li.active>a
    opacity 1

  .cd-morph-dropdown .morph-dropdown-wrapper
    display block
    top 58px
    width auto
    padding 0
    box-shadow none
    background-color transparent
    -webkit-transform translateZ(0)
    transform translateZ(0)
    will-change transform
    -webkit-transform translateY(20px)
    -ms-transform translateY(20px)
    transform translateY(20px)
    -webkit-transition -webkit-transform 0.3s
    transition -webkit-transform 0.3s
    transition transform 0.3s
    transition transform 0.3s, -webkit-transform 0.3s

  .cd-morph-dropdown.is-dropdown-visible .morph-dropdown-wrapper
    -webkit-transform translateY(0)
    -ms-transform translateY(0)
    transform translateY(0)

  .cd-morph-dropdown .dropdown-list
    position absolute
    top 0
    left 0
    visibility hidden
    -webkit-transform translateZ(0)
    transform translateZ(0)
    will-change transform, width, height
    -webkit-transition visibility 0.3s
    transition visibility 0.3s
    box-shadow 0 10px 20px rgba(0, 0, 0, 0.08)

  .no-csstransitions .cd-morph-dropdown .dropdown-list
    display none

  .cd-morph-dropdown .dropdown-list::before
    content ''
    position absolute
    bottom 100%
    left 50%
    right auto
    -webkit-transform translateX(-50%)
    -ms-transform translateX(-50%)
    transform translateX(-50%)
    height 0
    width 0
    border 8px solid transparent
    border-bottom-color #fff
    opacity 0
    -webkit-transition opacity 0.3s
    transition opacity 0.3s

  .cd-morph-dropdown .dropdown-list>ul
    position relative
    z-index 1
    height 100%
    width 100%
    overflow hidden

  .cd-morph-dropdown.is-dropdown-visible .dropdown-list
    visibility visible
    -webkit-transition width 0.3s, height 0.3s, -webkit-transform 0.3s
    transition width 0.3s, height 0.3s, -webkit-transform 0.3s
    transition transform 0.3s, width 0.3s, height 0.3s
    transition transform 0.3s, width 0.3s, height 0.3s, -webkit-transform 0.3s

  .cd-morph-dropdown.is-dropdown-visible .dropdown-list::before
    opacity 1

  .cd-morph-dropdown .dropdown
    position absolute
    left 0
    top 0
    opacity 0
    visibility hidden
    width 100%
    -webkit-transition opacity 0.3s, visibility 0.3s
    transition opacity 0.3s, visibility 0.3s

  .cd-morph-dropdown .dropdown.active
    opacity 1
    visibility visible

  .cd-morph-dropdown .dropdown.move-left .content
    -webkit-transform translateX(-100px)
    -ms-transform translateX(-100px)
    transform translateX(-100px)

  .cd-morph-dropdown .dropdown.move-right .content
    -webkit-transform translateX(100px)
    -ms-transform translateX(100px)
    transform translateX(100px)

  .cd-morph-dropdown .label
    display none

  .cd-morph-dropdown .content
    padding 2.2em 1.8em
    -webkit-transition -webkit-transform 0.3s
    transition -webkit-transform 0.3s
    transition transform 0.3s
    transition transform 0.3s, -webkit-transform 0.3s
    text-align left

  .cd-morph-dropdown .content>ul::after
    clear both
    content ''
    display block

  .cd-morph-dropdown .content>ul>li
    width 48%
    float left
    margin-right 4%
    margin-top 0

  .cd-morph-dropdown .content>ul>li:nth-of-type(2n)
    margin-right 0

  .cd-morph-dropdown .gallery .content
    width 510px
    padding-bottom 0.8em

  .cd-morph-dropdown .gallery .content li
    margin-bottom 1.8em

  .cd-morph-dropdown .links .content>ul>li
    margin-top 0

  .cd-morph-dropdown .links .content, .cd-morph-dropdown .button .content
    width 390px

  .cd-morph-dropdown .links-list a
    font-size 1.6rem
    margin-left 0

  .cd-morph-dropdown .btn
    display block
    width 100%
    height 60px
    margin 1.5em 0 0
    font-size 1.8rem
    text-align center
    color #fff
    line-height 60px
    background #db6356
    -webkit-font-smoothing antialiased
    -moz-osx-font-smoothing grayscale

  .cd-morph-dropdown .btn:hover
    background #1a1a1a
    color #fff

  .cd-morph-dropdown .content h2
    font-size 1.8rem
    text-transform none
    font-weight 400
    color #1a1a1a
    margin 0 0 0.6em

  .cd-morph-dropdown .bg-layer
    position absolute
    top 0
    left 0
    height 100%
    width 100%
    z-index -1
    background #fff
    opacity 0
    -webkit-transition all 0.3s
    transition all 0.3s
    -webkit-transform-origin top left
    -ms-transform-origin top left
    transform-origin top left
    -webkit-transform translateZ(0)
    transform translateZ(0)
    will-change transform
    -webkit-backface-visibility hidden
    backface-visibility hidden

  .cd-morph-dropdown.is-dropdown-visible .bg-layer
    opacity 1
    -webkit-transition all 0.3s, -webkit-transform 0.3s
    transition all 0.3s, -webkit-transform 0.3s
    transition transform 0.3s, opacity 0.3s
    transition transform 0.3s, opacity 0.3s, -webkit-transform 0.3s

.cd-main-content
  min-height 100vh
  background-color #548c7e

@media only screen and (min-width: 1000px)
  .cd-main-content
    padding-top 80px
</style>
