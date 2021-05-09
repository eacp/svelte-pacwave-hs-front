<script lang="ts">

	const url = "https://pacwave-leaderboard-dotnet.azurewebsites.net/api/hs";

	// The data from the store
	interface Score {
		score: number;
		playerName: string;
		timestamp: string;
	}

	let scores: Score[] = [];

	function getData() {
		// Make the fetch
		fetch(url)
			.then(res => res.json())
			.then((data: Score[]) => scores = data)
			.catch(() => {
				alert("Sorry, could not retrieve the scores");
			});
	}


	getData();
</script>

<main class="container">
	<div class="px-4 py-5 my-5 text-center">
		<img class="d-block mx-auto mb-4" src="https://getbootstrap.com/docs/5.0/assets/brand/bootstrap-logo.svg" alt="" width="72" height="57">
		<h1 class="display-5 fw-bold">High Score</h1>
		<div class="col-lg-6 mx-auto">
		  <p class="lead mb-4">Here are the high scores</p>
		  <div class="d-grid gap-2 d-sm-flex justify-content-sm-center">
			<button type="button" class="btn btn-primary btn-lg px-4 me-sm-3" on:click={getData}>Update</button>
		  </div>
		</div>
	  </div>

	  <table class="table table-dark table-striped">
		<thead>
	  <tr>
		<th scope="col">#</th>
		<th scope="col">Name</th>
		<th scope="col">Score</th>
		<th scope="col">Date</th>
	  </tr>
	</thead>
	<tbody>
	  {#each scores as row, i}
		  <tr>
			<th scope="row">{i+1}</th>
			<td> {row.playerName} </td>
			<td> {row.score} </td>
			<td> {new Date(row.timestamp)} </td>
		  </tr>
	  {/each}

	</tbody>
  
	</table>

</main>