<script lang="ts">
	type Options = 'one-way' | 'return'

	function handleSubmit(e: Event) {
		e.preventDefault()
		let prompt = `A ${tripType} trip has been booked. Departure date ${departureDate}.`
		if (tripType === 'return') {
			prompt += ` Return date ${returnDate}.`
		}
		alert(prompt)
	}

	function getDate() {
		const date = new Date()
		const [month, day, year] = date
			.toLocaleDateString('en-US', { year: 'numeric', month: '2-digit', day: '2-digit' })
			.split('/')
		return `${year}-${month}-${day}`
	}

	function isValidDate(d: string) {
		const date = new Date(d)
		return date.getTime() === date.getTime()
	}

	let tripType = $state<Options>('one-way')
	let departureDate = $state(getDate())
	let returnDate = $state(getDate())
</script>

<form onsubmit={handleSubmit} class="grid-gap">
	<div class="flex-col">
		<select name="return-flight" bind:value={tripType}>
			<option value="one-way">one-way</option>
			<option value="return">return</option>
		</select>

		<label>
			<span class="sr-only">Select departure date:</span>
			<input type="date" bind:value={departureDate} required min={getDate()} />
		</label>

		<label>
			<span class="sr-only">Select return date:</span>
			<input
				type="date"
				bind:value={returnDate}
				disabled={tripType !== 'return'}
				required
				min={getDate()}
			/>
		</label>

		<button
			type="submit"
			disabled={!departureDate ||
				!isValidDate(departureDate) ||
				(tripType === 'return' &&
					(departureDate > returnDate || !returnDate || !isValidDate(returnDate)))}>Book</button
		>
	</div>
</form>
