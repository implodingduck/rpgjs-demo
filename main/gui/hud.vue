<template>
    <div class="health-bar">
        <p>{{ x }} / {{ y }} / {{ z }} ( {{ direction }} )</p>
        <div class="bar">
            <div class="inner-bar" :style="{ width }"></div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'my-hud',
    inject: ['rpgCurrentPlayer'],
    data() {
        return {
            x: 0,
            y: 0,
            z: 0,
            direction: ""
        }
    },
    mounted() {
        this.obsCurrentPlayer = this.rpgCurrentPlayer
            .subscribe(({ object }) => {
                this.x = object.position.x
                this.y = object.position.y
                this.z = object.position.z
                this.direction = object.direction
            })
    },
    computed: {
        width() {
            //return ((this.hp / this.maxHp) * 100) + '%'
            return (1 * 100) + '%'
        }
    },
    unmounted() {
        this.obsCurrentPlayer.unsubscribe()
    }
}
</script>

<style>
.health-bar {
    width: 200px;
    margin-top: 10px;
    margin-left: 10px;
    background: rgba(0, 0, 0, 0.3)
}

.health-bar p {
    margin: 5px;
    color: white;
    font-size: 21px;
    font-weight: bold;
}

.bar {
    border: 2px solid black;
    border-radius: 5px;
    position: relative;
}

.inner-bar {
  background: #c54;
  height: 10px;
  position: relative;
  transition: width .5s linear;
}
</style>