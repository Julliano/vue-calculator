<template>
    <div class="calculator">
        <display :value="displayValue" />
        <customButton @on-calc-clicked="clearMemory" label="AC" triple />
        <customButton @on-calc-clicked="setOperation" label="/" operation />
        <customButton @on-calc-clicked="addDigit" label="7" />
        <customButton @on-calc-clicked="addDigit" label="8" />
        <customButton @on-calc-clicked="addDigit" label="9" />
        <customButton @on-calc-clicked="setOperation" label="*" operation />
        <customButton @on-calc-clicked="addDigit" label="4" />
        <customButton @on-calc-clicked="addDigit" label="5" />
        <customButton @on-calc-clicked="addDigit" label="6" />
        <customButton @on-calc-clicked="setOperation" label="-" operation />
        <customButton @on-calc-clicked="addDigit" label="1" />
        <customButton @on-calc-clicked="addDigit" label="2" />
        <customButton @on-calc-clicked="addDigit" label="3" />
        <customButton @on-calc-clicked="setOperation" label="+" operation />
        <customButton @on-calc-clicked="addDigit" label="0" double />
        <customButton @on-calc-clicked="addDigit" label="." />
        <customButton @on-calc-clicked="setOperation" label="=" operation />
    </div>
</template>

<script>
    import display from '../components/display';
    import customButton from '../components/button';

    export default {
        components: {
            customButton,
            display
        },
        data() {
            return {
                displayValue: '0',
                clearDisplay: false,
                operation: null,
                values: [0, 0],
                current: 0
            }
        },
        methods: {
            clearMemory() {
                Object.assign(this.$data, this.$options.data());
            },
            setOperation(operation) {
                if (this.current === 0) {
                    this.operation = operation;
                    this.current = 1;
                    this.clearDisplay = true;
                } else {
                    const equals = operation === '=';
                    const currentOperation = this.operation;

                    try {
                        this.values[0] = eval (
                            `${this.values[0]} ${currentOperation} ${this.values[1]}`
                        )
                    } catch (e) {
                        this.$emit('onError', e);
                    }

                    this.values[1] = 0;

                    this.displayValue = this.values[0];
                    this.operation = equals ? null : operation;
                    this.current = equals ? 0 : 1;
                    this.clearDisplay = !equals;
                }
            },
            addDigit(n) {
                if (n === '.' && this.displayValue.includes('.')) return;
                
                const clearDisplay = this.displayValue === '0' || this.clearDisplay;
                const currentValue = clearDisplay ? '' : this.displayValue;
                const displayValue = currentValue + n;
                
                this.displayValue = displayValue;
                this.clearDisplay = false;

                // 1 alternative
                this.values[this.current] = displayValue;

                // 2 alternative
                // if (n !== '.') {
                //     const i = this.current;
                //     const newValue = parseFloat(displayValue);
                //     this.values[i] = newValue;
                // }
            }
        }
    }
</script>

<style>
  .calculator {
    height: 320px;
    width: 235px;
    border-radius: 5px;
    overflow: hidden;
    display: grid;
    grid-template-columns: repeat(4, 25%);
    grid-template-rows: 1fr 48px 48px 48px 48px 48px;
  }
</style>
