<template>
    <div class="sidemenu">
        <div @click="toggle()" ref="removable" :class="['removable', this.extended === true ? 'extended' : '']">
            <div class="title">
                Get Started
            </div>

            <div ref="menubody" :class="['body', this.extended === true ? 'extended' : '']">
                <div class="navbutton" @click="navigate($event, link.route)" v-for="link of nav">
                    {{ link.title }}
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        props: {
            nav: {
                type: Array,
                default() {
                    return [
                        {
                            title: 'Home',
                            route: '/'
                        },
                        {
                            title: 'Learn Genders',
                            route: 'genders'
                        },
                        {
                            title: 'Conjugation Practice',
                            route: 'conjugate'
                        }
                    ];
                }
            }
        },
        data() {
            return {
                extended: false
            };
        },
        methods: {
            toggle() {
                this.extended = !this.extended;
            },
            navigate(e, route) {
                e.stopPropagation();

                this.extended = false;
                this.$router.push(route);
            }
        }
    };
</script>

<style lang="scss" scoped>
    $start-width: 3em;

    .sidemenu {
        width: $start-width;
        height: 100%;

        .removable {
            transition: 500ms;
            background: $menu-base;
            width: $start-width;
            height: 100%;

            position: absolute;

            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-direction: row;
            right: 0;

            &.extended {
                width: 20em;
            }

            .title {
                writing-mode: vertical-rl;
                text-orientation: mixed;
                color: white;
                user-select: none;
                padding: 1em;
            }

            .body {
                transition: 500ms;
                width: 0;
                opacity: 0;
                padding: 0;
                height: 100%;
                cursor: auto;
                background: $menu-darker;

                &.extended {
                    width: auto;
                    flex-grow: 1000;
                    opacity: 1;
                }

                .navbutton {
                    width: 100%;
                    color: white;
                    height: 3em;
                    user-select: none;
                    cursor: pointer;
                    line-height: 3em;

                    border-top: 1px solid $menu-darker;
                    border-bottom: 1px solid $menu-darker;
                    transition: 300ms;
                    background: $menu-base;
                    white-space: pre;
                    overflow: hidden;
                    text-overflow: clip;

                    &:hover {
                        filter: brightness(.95);
                    }
                }
            }
        }
    }
</style>