<template>
    <label class="toggle__button" :class="{'active': isActive}">
        <span v-if="isActive" class="toggle__label">{{ enableText }}</span>
        <span v-if="!isActive" class="toggle__label">{{ disabledText }}</span>

        <input type="checkbox" v-model="checkedValue" :disabled="disabled">
        <span class="toggle__switch"></span>
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
        url: String,
        formInputs: Object,
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
.active {
    .toggle__switch {
        background: #adedcb;
        box-shadow: inset 0 0 1px #adedcb;

        &::after, &::before {
            transform:translateX(40px - 18px);
        }

        &::after {
            left: 6px;
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

    &__label {

    }

    &__switch {
        display:inline-block;
        height:12px;
        border-radius:6px;
        width:40px;
        background: #BFCBD9;
        box-shadow: inset 0 0 1px #BFCBD9;
        position:relative;
        margin-left: 10px;
        transition: all .25s;

        &::after {
            background: #4D4D4D;
            box-shadow: 0 0 1px #666;
        }

        &::before {
            background: #4D4D4D;
            box-shadow: 0 0 0 3px rgba(0,0,0,0.1);
            opacity:0;
        }

        &::after, &::before {
            content: "";
            position: absolute;
            display: block;
            height: 18px;
            width: 18px;
            border-radius: 50%;
            left: 0;
            top: -3px;
            transform: translateX(0);
            transition: all .25s cubic-bezier(.5, -.6, .5, 1.6);
        }
    }
}
</style>