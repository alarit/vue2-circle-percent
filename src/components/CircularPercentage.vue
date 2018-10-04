<template>
    <div>
        <div class="flex-wrapper">
            <svg :viewBox=viewBox class="circular-chart">
                <path class="circle" :style=circleStroke :d=circlePath />
                <path class="completed-arc" :style=arcStroke :stroke-dasharray=dashArray :d=circlePath />
                <text :x=box/2 :y=(diameter/2+textSize/2)+1 class="percentage" :style=fontTextSize>{{percentage}}%</text>
            </svg>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'CircularPercentage',
        props: {
            size: {
                size: Number,
                default: 100
            },
            done: {
                type: Number,
                required: true
            },
            missing: {
                type: Number,
                required: true
            },
            arcColor: {
                type: String,
                default: '#00c71b'
            },
            bgCircleColor: {
                type: String,
                default: '#00cc1b33',
            }
        },
        computed: {
            percentage() {
                return parseFloat(100 / (this.done + this.missing) * this.done).toFixed(1);
            },
            dashArray() {
                let perc = this.size / 100 * this.percentage;
                return perc + ', ' + this.size;
            },
            radius() {
                return this.size / (2 * 3.14159);
            },
            diameter() {
                return this.radius * 2;
            },
            box() {
                return 36;
            },
            viewBox() {
                return '0 0 ' + this.box + ' ' + this.box;
            },
            circlePath() {
                return 'M' + (this.box / 2) + ' 2.08' /*([this.box - this.diameter] / 2)*/
                    + ' a ' + this.radius + ' ' + this.radius + ' 0 0 1 0 ' + this.diameter
                    + ' a ' + this.radius + ' ' + this.radius + ' 0 0 1 0 -' + this.diameter;

            },
            textSize() {
                return this.size / 11;
            },
            fontTextSize() {
                return 'font-size: ' + this.textSize + 'px';
            },
            arcStroke() {
                return 'stroke: ' + this.arcColor;
            },
            circleStroke() {
                return 'stroke: ' + this.bgCircleColor;
            }
        }
    }
</script>

<style scoped>
    .flex-wrapper {
        display: flex;
        flex-flow: row nowrap;
    }

    .circular-chart {
        max-width: 90%;
        max-height: 200px;
        margin: 5px auto;
    }

    .circle {
        fill: none;
        stroke-width: 2.0;
    }

    .completed-arc {
        fill: none;
        stroke-width: 1.3;
        stroke-linecap: round;
        animation: progress 2s ease-out forwards;
    }

    @keyframes progress {
        0% {
            stroke-dasharray: 0 100;
        }
    }

    .percentage {
        fill: #666164;
        text-anchor: middle;
    }
</style>
