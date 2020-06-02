<template>
    <div class="field">
        <label class="label">{{ label }} <small v-if="required">({{ $t('fields.required')}})</small></label>
        <div class="control">
            <input class="input"
                   :class="error ? 'is-danger' : ''"
                   :list="options ? 'datalist'+label.replace(/ /g,'') : null"
                   :type="type"
                   v-model="inputValue"
                   :required="required"
                   :min="min"
                   :max="max"
                   :maxlength="maxlength"
                   @blur="$emit('blur', true)"
                   :disabled="disabled" />
            <p class="help" v-if="help && !error">{{ help }}</p>
            <p class="help is-danger" v-if="error">{{ error }}</p>
            <datalist :id="'datalist'+label.replace(/ /g,'')" v-if="options">
                <option v-for="option in options" :key="option">{{ option }}</option>
            </datalist>
        </div>
    </div>

</template>

<script>

    export default {
        props: ["label","type","help","required","value","min","max","options","disabled","error","required","maxlength","charReplace"],
        computed: {
            inputValue: {
                get() {
                    let value = this.value;
                    if(value && this.charReplace) {
                        let pattern = new RegExp(this.charReplace,"g");
                        value = value.replace(pattern, '');
                    }
                    return value
                },
                set(val) {
                    this.$emit('input', val);
                    if(this.options) {
                        for (let i = 0; i < this.options.length; i++) {
                            if (this.options[i] === val) {
                                this.$emit('blur', true);
                            }
                        }
                    }
                }
            }
        },
    }
</script>
