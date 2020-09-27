<template>
    <div class="container" :class="{'show': showSidebar}">
        <div class="control">
            <i class="fa fa-bars fa-fw" @click="showNav"></i>
        </div>
        <div class="navigation-icons">
            <i class="fa fa-money"></i>
            <i class="fa fa-bus"></i>
            <i class="fa fa-graduation-cap"></i>
            <i class="fa fa-money"></i>
            <i class="fa fa-graduation-cap"></i>
            <i class="fa fa-bus"></i>
        </div>
        <div class="navigation-links">
            <transition-group name="fade">
                <div v-show="showLink" key="1">Sports</div>
                <div v-show="showLink" key="2">Travel</div>
                <div v-show="showLink" key="3">Food</div>
                <div v-show="showLink" key="4">Money</div>
                <div v-show="showLink" key="5">Education</div>
                <div v-show="showLink" key="6">Volunteering</div>
            </transition-group>
        </div>
    </div>
    
</template>

<script>
export default {
    name: "SideBarComponent",
    data: () => {
        return {
            showSidebar: false,
            showLink: false,
        }
    },
    methods: {
        showNav() {
            if (this.showSidebar) {
             this.showLink = false;
             setTimeout (()=>{
                 this.showSidebar = false;
             },500);
            }
            else {
                this.showSidebar = true;
             setTimeout (()=> {
                 this.showLink = true;
             },500)
            }
        }
    }
}
</script>

<style lang="scss" scoped>
    $fa-font-path: "~font-awesome/fonts" !default;
    @import '~font-awesome/scss/font-awesome';

    .container {
        position: absolute;
        top: 0;
        left: 0;
        width: 70px;
        padding: 10px;
        min-height: calc(100vh - 1px);
        background-color: rgba($color: #3498DB, $alpha: 0.8);
        border: solid #fff;
        border-width: 0 1px 0 0;
        z-index: 999;
        transition: all .5s ease-in-out;

        .control {
            display: flex;
            justify-content: center;
            align-items: center;
            width: 50px;
            margin-bottom: 10px;

            i {
            font-size: 2rem;
            cursor: pointer;
            transition: all .5s ease-in-out;
            }
        }

        &.show {
            width: 180px;

            .control > i {
                color: #fff;
                transform: rotateZ(-90deg);
            }

            .navigation-icons {
                color: #fff;
            }
        }

        .navigation-icons {
            display: flex;
            justify-content: center;
            align-items: center;
            flex-direction: column;
            width: 50px;
            float: left;

            i {
                font-size: 2rem;
                padding: 10px 0;
                cursor: pointer;
                transition: all .5s ease-in-out;

                &:hover {
                    color: #fff;
                }
            }
        }

        .navigation-links {
            padding-top: 14px;
            float: left;

            div {
                font-size: 1.35 rem;
                font-weight: 600;
                padding-left: 10px;
                margin-bottom: 30px;
                cursor: pointer;

                &:hover {
                    color: #fff;

                }
            }
        }
    }

    @mixin nav-childs($values...) {
        @each $var in $values {
            &:nth-child(#{$var}) {
                transition: transform linear calc(.1s * #{$var}), display .5s;
            }
        }
    }

    .fade-enter-active, .fade-leave-active {
        @include nav-childs(1,2,3,4,5);
    }

    .fade-enter, .fade-leave-to {
        transform: scale(0);
    }

</style>