<script>
	import { onMount } from 'svelte';

	let rating = 0;

	const handleRatingChange = (e) => {
		rating = e.target.value;
	};

	const addClassToChecked = () => {
		const checked = document.querySelector('input[type="radio"]:checked');
		const labels = document.querySelectorAll('.radio-label');
		labels.forEach((label) => {
			label.classList.remove('checked');
		});
		checked.parentElement.classList.add('checked');
	};

	onMount(() => {
		const stars = document.querySelectorAll('input[type="radio"]');
		stars.forEach((star) => {
			star.addEventListener('change', (e) => {
				const rating = e.target.value;
				stars.forEach((star) => {
					star.checked = false;
				});
				for (let i = 0; i < rating; i++) {
					stars[i].checked = true;
				}
			});
		});

		const submitBtn = document.querySelector('button');
		submitBtn.addEventListener('click', (e) => {
			if (rating === 0) {
				alert('Please select a rating');
			}
		});

		const labels = document.querySelectorAll('.radio-label');
		labels.forEach((label) => {
			label.addEventListener('click', (e) => {
				addClassToChecked();
			});
		});

		// when submit button is clicked and rating is not 0 then show thank you container and hide rating container
		submitBtn.addEventListener('click', (e) => {
			if (rating !== 0) {
				const ratingContainer = document.querySelector('.rating-container');
				const thankYouContainer = document.querySelector('.thank-you-container');
				ratingContainer.classList.add('hidden');
				thankYouContainer.classList.remove('hidden');
			}
		});
	});
</script>

<svelte:head>
	<title>Interactive Rating Component 🌟</title>
</svelte:head>

<main class="flex justify-center items-center h-[100vh] bg-very-dark-blue">
	<div class="rating-container w-[450px] bg-dark-grey p-10 rounded-3xl">
		<img
			src="../../images/icon-star.svg"
			alt="star rating icon"
			class="bg-dark-blue rounded-full w-10 h-10 p-3 mb-5"
		/>
		<h2 class="text-white text-2xl mb-5 font-overpass">How did we do?</h2>
		<p class="text-light-grey font-overpass mb-5">
			Please let us know how we did with your support request. All feedback is appreciated to help
			us improve our offering!
		</p>
		<form action="">
			<div>
				<div class="flex text-light-grey mb-8 justify-between">
					{#each [1, 2, 3, 4, 5] as star}
						<label
							class="bg-dark-blue rounded-full p-3 w-12 h-12 text-center cursor-pointer radio-label hover:text-white hover:bg-primary transition-all"
						>
							<input
								type="radio"
								name="rating"
								value={star}
								class="hidden"
								on:change={handleRatingChange}
							/>
							{star}
						</label>
					{/each}
				</div>
			</div>
			<button
				class="text-white bg-primary w-full rounded-full py-3 font-overpass text-sm tracking-wides hover:bg-white hover:text-primary transition-all duration-300"
				>SUBMIT</button
			>
		</form>
	</div>
	<div class="thank-you-container w-[450px] bg-dark-grey p-10 rounded-3xl hidden">
		<div class="flex justify-center">
			<img
				src="../../images/illustration-thank-you.svg"
				alt="Illustration of a phone receiving feedback"
				class="w-40 mb-8"
			/>
		</div>
		<div class="flex justify-center">
			<p class="text-primary bg-dark-blue text-center mb-5 rounded-full py-2 px-6">
				You Selected {rating} out of 5
			</p>
		</div>
		<h2 class="text-white text-2xl mb-5 font-overpass text-center">Thank you!</h2>
		<p class="text-light-grey font-overpass mb-5 text-center">
			We appreciate you taking the time to give a rating. If you ever need more support, don't
			hesitate to get in touch!
		</p>
	</div>
</main>
