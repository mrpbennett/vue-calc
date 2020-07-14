<template>
    <div class="calc uppercase p-4 text-lg  shadow">
        <div
            class="col-span-4 text-right pr-4 text-gray-100 text-5xl font-black display"
        >
            <div>
                <div class="flex pl-1">
                    <div
                        class="rounded-full h-3 w-3 mr-1"
                        style="background-color: #FF5F57"
                    ></div>
                    <div
                        class="rounded-full bg-black h-3 w-3 mr-1"
                        style="background-color: #FFBD2E"
                    ></div>
                    <div
                        class="rounded-full bg-black h-3 w-3"
                        style="background-color: #28CA42"
                    ></div>
                </div>
            </div>
            <div class="pt-16 flex flex-col">
                <span class="text-sm text-right font-normal tracking-wide">{{
                    calculation || 0
                }}</span>
                {{ current || 0 }}
            </div>
        </div>

        <div class="calc-buttons">
            <div @click="clear" class="btn">c</div>
            <div @click="sign" class="btn">+/-</div>
            <div @click="percent" class="btn">%</div>
            <div @click="divide" class="btn op">/</div>
            <div @click="append('7')" class="btn">7</div>
            <div @click="append('8')" class="btn">8</div>
            <div @click="append('9')" class="btn">9</div>
            <div @click="multiply" class="btn op">
                <svg
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 20 20"
                    class="
                h-5 w-5 fill-current"
                >
                    <path
                        d="M10 8.586L2.929 1.515 1.515 2.929 8.586 10l-7.071 7.071 1.414 1.414L10 11.414l7.071 7.071 1.414-1.414L11.414 10l7.071-7.071-1.414-1.414L10 8.586z"
                    />
                </svg>
            </div>
            <div @click="append('4')" class="btn">4</div>
            <div @click="append('5')" class="btn">5</div>
            <div @click="append('6')" class="btn">6</div>
            <div @click="subtract" class="btn op">-</div>
            <div @click="append('1')" class="btn">1</div>
            <div @click="append('2')" class="btn">2</div>
            <div @click="append('3')" class="btn">3</div>
            <div @click="add" class="btn op">+</div>
            <div @click="append('0')" class="btn">0</div>
            <div @click="dot" class="btn">.</div>
            <div @click="backspace" class="btn">
                <svg
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 20 20"
                    class="
                h-6 w-6 fill-current"
                >
                    <path
                        d="M0 10l7-7h13v14H7l-7-7zm14.41 0l2.13-2.12-1.42-1.42L13 8.6l-2.12-2.13-1.42 1.42L11.6 10l-2.13 2.12 1.42 1.42L13 11.4l2.12 2.13 1.42-1.42L14.4 10z"
                    />
                </svg>
            </div>
            <div @click="equal" class="btn">=</div>
        </div>
    </div>
</template>

<script>
    export default {
        data() {
            return {
                current: '',
                calculation: '',
                previous: null,
                operator: null,
                operatorClicked: false,
            };
        },
        methods: {
            clear() {
                this.current = '';
                this.calculation = '';
            },
            sign() {
                this.current =
                    this.current.charAt(0) === '-'
                        ? this.current.slice(1)
                        : `-${this.current}`;
            },
            percent() {
                this.current = `${parseFloat(this.current) / 100}`;
            },
            append(number) {
                if (this.operatorClicked) {
                    this.current = '';
                    this.operatorClicked = false;
                }
                this.current = `${this.current}${number}`;
                this.calculation = this.current;
            },
            dot() {
                if (this.current.indexOf('.') === -1) {
                    this.append('.');
                }
            },
            setPrevious() {
                this.previous = this.current;
                this.operatorClicked = true;
            },
            divide() {
                this.operator = (a, b) => a / b;
                this.setPrevious();
            },
            multiply() {
                this.operator = (a, b) => a * b;
                this.setPrevious();
            },
            subtract() {
                this.operator = (a, b) => a - b;
                this.setPrevious();
            },
            add() {
                this.operator = (a, b) => a + b;
                this.setPrevious();
            },
            equal() {
                this.current = `${this.operator(
                    parseFloat(this.current),
                    parseFloat(this.previous)
                )}`;
                this.previous = null;
            },
            backspace() {
                this.current = this.current.slice(0, -1);
                this.calculation = this.calculation.slice(0, -1);
            },
        },
    };
</script>

<style scoped>
    .calc {
        width: 300px;
        overflow: hidden;
        border-radius: 1.5rem;
        background-image: linear-gradient(to right, #6a11cb 0%, #2575fc 100%);
    }
    .calc-buttons {
        display: grid;
        grid-template-columns: repeat(4, 1fr);
        grid-auto-rows: minmax(50px, auto);
        color: #f7fafc;
    }
    .display {
        border-bottom: solid 2px rgba(255, 255, 255, 0.5);
    }

    .btn {
        display: flex;
        align-items: center;
        justify-content: center;
        font-weight: bold;
        font-size: 1.5rem;
        padding: 1rem;
    }
    .btn:hover {
        background-color: rgba(0, 0, 0, 0.2);
        cursor: pointer;
    }
</style>
