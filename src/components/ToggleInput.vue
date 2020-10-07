<template>
    <label class="toggle__button"
           :class="{'active': isActive, 'sm': size==='sm','lg': size==='lg','pointer-events-none': disabled }">
        <span v-if="isActive && labelShow" class="toggle__label">{{ enableText }}</span>
        <span v-if="!isActive && labelShow" class="toggle__label">{{ disabledText }}</span>

        <input type="checkbox" v-model="checkedValue" :disabled="disabled">
        <span class="toggle__switch"
              :class="{'sm': size === 'sm','lg': size==='lg', [disabledBgClass]: !isActive, [enabledBgClass]: isActive }"
              :style="disabled ? 'opacity:0.5' : ''"></span>
    </label>
</template>

<script>
export default {
    name: "ToggleInput",
    props: {
        defaultState: Number,
        disabled: {type: Boolean, default: false},
        labelEnableText: {type: String, default: 'On'},
        labelDisableText: {type: String, default: 'Off'},
        labelShow: {type: Boolean, default: true},
        url: String,
        size: {type:String, default: 'sm'},
        formInputs: Object,
        disabledBgClass: {type: String, default: 'bg-off'},
        enabledBgClass: {type: String, default: 'bg-on'}
    },
    data() {
        return {
            currentState: this.defaultState
        }
    },
    computed: {
        isActive() {
            return this.currentState
        },
        enableText() {
            return this.labelEnableText;
        },
        disabledText() {
            return this.labelDisableText;
        },
        checkedValue: {
            get() {
                return this.currentState
            },
            set(newValue) {
                this.currentState = newValue;

                const form = new FormData();

                let inputs = this.formInputs;
                Object.keys(inputs).forEach(function (index) {
                    form.append(index,inputs[index]);
                });

                this.$http.post(this.url,form,{headers: {
                        "Content-Type": "application/x-www-form-urlencoded; charset=UTF-8",}})
                    .then(response => {
                        console.log(response.data);
                });
            }
        }
    }
}
</script>

<style scoped lang="scss">

.bg-on {
    background: #adedcb;
    box-shadow: inset 0 0 1px #bcf0d4;
}

.bg-off {
    background: #8c8c8c;
    box-shadow: inset 0 0 1px #949494;
}

.pointer-events-none {
    pointer-events: none;
}

label {
    &.lg {
        margin-bottom: 10px;
        margin-top: 10px;
    }

    &.sm {
        margin-bottom: 5px;
    }
}

.active {
    .toggle__switch {


        &::after, &::before {
            transform:translateX(40px - 18px);
        }

        &.lg::after {
            left: 26px;
        }

        &.sm::after {
            left: 6px;
        }

        &::after {
            background: #53B883;
            box-shadow: 0 0 1px #53B883;
        }
    }
}

.toggle {
    &__button {
        vertical-align: middle;
        user-select: none;
        cursor: pointer;

        input[type="checkbox"] {
            opacity: 0;
            position: absolute;
            width: 1px;
            height: 1px;
        }
    }

    &__switch {
        display:inline-block;
        position:relative;
        margin-left: 10px;
        margin-right: 10px;
        transition: all .25s;

        &.sm {
            height:12px;
            border-radius:6px;
            width:40px;
        }

        &.lg {
            height: 24px;
            border-radius: 12px;
            width: 80px;
        }

        &::after {
            background: #4D4D4D;
            box-shadow: 0 0 1px #666;
        }

        &::before {
            background: #4D4D4D;
            box-shadow: 0 0 0 3px rgba(0,0,0,0.1);
            opacity:0;
        }

        &.lg::after,&.lg::before {
            height: 36px;
            width: 36px;
            top: -6px;
        }

        &.sm::after,&.sm::before {
            height: 18px;
            width: 18px;
            top: -3px;
        }

        &::after, &::before {
            content: "";
            position: absolute;
            display: block;
            border-radius: 50%;
            left: 0;
            transform: translateX(0);
            transition: all .25s cubic-bezier(.5, -.6, .5, 1.6);
        }
    }
}
</style>