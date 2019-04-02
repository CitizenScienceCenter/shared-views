<template>
  <div>

  <div class="sub-navigation" ref="subnav">
      <ul ref="navlist">
        <li v-for="child in $router.options.routes.filter(x=>x.path==$route.matched[0].path)[0].children">
          <router-link :to="child.path" active-class="active" :ref="child.meta.i18n">{{ $t(child.meta.i18n+'.link') }}</router-link>
        </li>
      </ul>
    </div>

    <router-view platform></router-view>

  </div>
</template>

<script>

    export default {
        name: 'ChildView',
        props: {
            platform: {
                type: Boolean,
                default: false
            }
        },
        mounted() {
            this.navScroll();
            this.setCenteredIfNeeded();
        },
        updated() {
            if( this.$refs.subnav ) {
                this.navScroll();
                this.setCenteredIfNeeded();
            }
        },
        methods: {
            navScroll() {
                this.$refs.subnav.scrollLeft = 0;
                if( this.$refs[ this.$router.currentRoute.meta.i18n ][0].$el.offsetLeft + this.$refs[ this.$router.currentRoute.meta.i18n ][0].$el.offsetWidth > window.innerWidth ) {
                    this.$refs.subnav.scrollLeft = this.$refs[ this.$router.currentRoute.meta.i18n ][0].$el.offsetLeft;
                }
            },
            setCenteredIfNeeded() {
                if( this.$refs.navlist.offsetWidth <= window.innerWidth ) {
                    this.$refs.subnav.classList.add('centered');
                }
                else {
                    this.$refs.subnav.classList.remove('centered');
                }
            }
        }
    }

</script>

<style lang="scss">

  @import '@/styles/theme.scss';
  @import '@/styles/shared/variables.scss';

  .sub-navigation {
    padding: $spacing-1 0;
    overflow-x: auto;
    background-color: $color-black-tint-97;
    display: flex;

    &.centered {
      justify-content: center;
    }


    ul {
      display: flex;
      flex-wrap: nowrap;
      box-sizing: border-box;

      padding: 0 calc( #{$grid-margin-mobile} + #{$grid-gutter-mobile} / 2);

      li {
        white-space: nowrap;
        margin: 0;
        padding: 0;
        margin-right: $spacing-2;

        &:last-child {
          margin-right: 0;
        }

        &:before {
          display: none;
        }
        a {
          white-space: nowrap;
          display: block;
          font-size: $font-size-small;
          color: $color-black-tint-50;
          cursor: pointer;
          line-height: 40px;

          &:active {
            color: $color-black;
          }
          @media (hover: hover) {
            &:hover {
              color: $color-black;
            }
          }

          &.active {
            color: $color-black;
          }
        }
      }
    }
  }





  @media only screen and (min-width: $viewport-tablet-portrait) {

    .sub-navigation {
      justify-content: center;
      ul {
        li {
          margin-right: $spacing-3;
          &:last-child {
            margin-right: 0;
          }
          a {
            line-height: 48px;
          }
        }
      }
    }

  }



  @media only screen and (min-width: $viewport-large) {

    .sub-navigation {

      ul {
        li {
          margin-right: $spacing-4;
          &:last-child {
            margin-right: 0;
          }
        }
      }
    }

  }

</style>
