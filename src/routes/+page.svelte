<script lang="ts">
	import { goto } from '$app/navigation';
	import Banner from '$lib/Banner.svelte';

	let userId = '';
	let bannerInfo = {
		style: 'error',
		text: '',
		display: false
	};

	function showQuestions() {
		if (checkId()) {
			// window.location.href = `/survey?id=${userId}`;
			goto(`/survey?id=${userId}`);
		} else {
			bannerInfo.text = 'Please enter a valid ID';
			bannerInfo.display = true;
			setTimeout(() => {
				bannerInfo.display = false;
			}, 2000);
		}
	}

	function checkId(): boolean {
		try {
			const id = parseFloat(userId);
			if (id === Math.round(id) && id <= 100 && id >= 0) return true;
		} catch (error) {
			console.log(error);
		}

		return false;
	}
</script>

<svelte:head>
	<title>Group 14 Survey</title>
	<meta name="description" content="Survey on HCI" />
</svelte:head>

<section id="UserId">
	<h1>Welcome!</h1>

	<h2>Instructions</h2>

	<p>
		Thank you for agreeing to take part in our HCI experiment. Please ensure that you take part in
		this study completely alone. It will take approximately 10 minutes to complete and you will be
		asked to classify 10 short stories. <br /><br />

		You will firstly be asked to enter your user ID - this should have been provided to you before
		the experiment. As your proceed from there you will be presented a story generated by a
		computer. This same story will also be inputted and classified by an AI and the emotion(s) it
		thinks is being displayed most will be shown to you. <br /><br />

		Following this you will select from a finite list of emotions the emotion you think best matches
		what was conveyed in the story above.<br /><br />

		In order for us to build a better understanding, we ask you to write a short answer reasoning
		why you selected the emotion.<br /><br />

		Finally, select on the slider the confidence level of your answer. 0% (left) being not confident
		at all and 100% (right) being very confident.<br />
	</p>
	<h3>Enter your user ID</h3>

	<input class="userId" bind:value={userId} placeholder="ID" />

	<hr />

	<h2>Research Consent Form</h2>
	<h3>THIS FORM WILL BE HELD FOR A PERIOD OF 2 MONTHS</h3>

	<p>
		Project title: Visualising and supporting uncertainty in emotion recognition displays<br />
		Name of Supervisor: Danielle Lottridge<br />
		Name of Student Researcher: Gerald Webber
	</p>

	<p>
		I have read the Participant Information Sheet, have understood the nature of the research and
		why I have been selected. I have had the opportunity to ask questions and have had them answered
		to my satisfaction.
		<br />
		<br />
		• I agree to take part in this research. <br />
		• I understand that I am free to withdraw my participation at any time, and to withdraw any data
		traceable.<br />
		• I wish / do not wish to receive the summary of findings.<br />
		• I agree to not disclose anything discussed in the focus group.<br />
	</p>

	<button on:click={() => showQuestions()} class="proceed"> Agree and Proceed </button>
</section>

<Banner {bannerInfo} />
