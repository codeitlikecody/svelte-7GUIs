<script lang="ts">
	class Temperature {
		// default state temp of freezing water
		#celsius = $state(0)
		#fahrenheit = $state(32)

		get celsius() {
			return this.#celsius
		}

		set celsius(c) {
			this.#celsius = c

			// F = C * (9/5) + 32
			this.#fahrenheit = c * (9 / 5) + 32
		}

		get fahrenheit() {
			return this.#fahrenheit
		}

		set fahrenheit(f) {
			this.#fahrenheit = f

			// C = (F - 32) * (5/9)
			this.#celsius = (f - 32) * (5 / 9)
		}
	}

	const temperature = new Temperature()
</script>

<div class="flex-col">
	<div class="flex-gap">
		<input type="number" bind:value={temperature.celsius} /> Celsius
	</div>
	<div class="flex-gap">
		<input type="number" bind:value={temperature.fahrenheit} /> Fahrenheit
	</div>
</div>

<style>
	input[type='number'] {
		max-width: 10ch;
	}
</style>
