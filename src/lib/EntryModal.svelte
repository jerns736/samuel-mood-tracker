<script>
	import supabase from '$lib/db';
	let emojiList = {
		Worst: '😭',
		Bad: '🙁',
		Okay: '😐',
		Good: '🙂',
		Best: '😁'
	};
	let emoji = '😐';
	let day = '1';
	let month = '1';
	let year = '2021';
	let mood = 'Okay';
	let comment = 'This is a comment';

	// Insert entry
	async function saveEntry() {
		const { error } = await supabase.from('moodEntries').insert({
			user_id: supabase.auth.user().id,
			day: day,
			month: month,
			year: year,
			mood: mood,
			comment: comment
		});
		if (error) alert(error.message);

		location.reload(); // Refresh the page.
	}
</script>

<div class="modal fade" id="newEntry" tabindex="-1">
	<div class="modal-dialog modal-dialog-centered modal-dialog-scrollable">
		<div class="modal-content">
			<div class="modal-header">
				<h5 class="modal-title">New Entry</h5>
				<button type="button" class="btn-close" data-bs-dismiss="modal" />
			</div>

			<div class="modal-body">
				<!-- Add Modal Content here -->
				<!-- Date Input -->
				<div class="row">
					<div class="col">
						<form class="form-floating">
							<input
								type="number"
								class="form-control"
								id="dayInput"
								bind:value={day}
								min="1"
								max="31"
							/>
							<label for="dayInput">Day</label>
						</form>
					</div>
					<div class="col">
						<form class="form-floating">
							<input
								type="number"
								class="form-control"
								id="monthInput"
								bind:value={month}
								min="1"
								max="12"
							/>
							<label for="monthInput">Month</label>
						</form>
					</div>
					<div class="col">
						<form class="form-floating">
							<input
								type="number"
								class="form-control"
								id="yearInput"
								bind:value={year}
								min="2021"
							/>
							<label for="yearInput">Year</label>
						</form>
					</div>
				</div>
				<!-- Mood Scale -->
				<div class="row mt-3 text-center">
					<h5>How was your day?</h5>
					<h1 class="display-1">{emoji}</h1>
				</div>
				<div class="row px-5">
					<div class="btn-group mt-2 mb-3" role="group">
						<!-- Worst Mood -->
						<input
							type="radio"
							class="btn-check"
							name="moodRadio"
							id="Worst"
							autocomplete="off"
							on:click={() => {
								emoji = emojiList.Worst;
								mood = 'Worst';
							}}
						/>
						<label class="btn btn-outline-danger" for="Worst">Worst</label>
						<!-- Bad Mood -->
						<input
							type="radio"
							class="btn-check"
							name="moodRadio"
							id="Bad"
							autocomplete="off"
							on:click={() => {
								emoji = emojiList.Bad;
								mood = 'Bad';
							}}
						/>
						<label class="btn btn-outline-warning" for="Bad">Bad</label>
						<!-- Okay Mood -->
						<input
							type="radio"
							class="btn-check"
							name="moodRadio"
							id="Okay"
							autocomplete="off"
							on:click={() => {
								emoji = emojiList.Okay;
								mood = 'Okay';
							}}
						/>
						<label class="btn btn-outline-primary" for="Okay">Okay</label>
						<!-- Good Mood -->
						<input
							type="radio"
							class="btn-check"
							name="moodRadio"
							id="Good"
							autocomplete="off"
							on:click={() => {
								emoji = emojiList.Good;
								mood = 'Good';
							}}
						/>
						<label class="btn btn-outline-info" for="Good">Good</label>
						<!-- Best Mood -->
						<input
							type="radio"
							class="btn-check"
							name="moodRadio"
							id="Best"
							autocomplete="off"
							on:click={() => {
								emoji = emojiList.Best;
								mood = 'Best';
							}}
						/>
						<label class="btn btn-outline-success" for="Best">Best</label>
					</div>
				</div>
				<!-- Comments -->
				<div class="form-floating">
					<textarea bind:value={comment} class="form-control" id="comment" />
					<label for="commentTextarea">Comments</label>
				</div>
			</div>

			<div class="modal-footer">
				<button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Cancel</button>
				<button type="button" class="btn btn-primary" on:click={saveEntry}>Add</button>
			</div>
		</div>
	</div>
</div>
