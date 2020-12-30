<script>
	const bands = [
		{ name: 'Small',  users: 2,  price: 240, },
		{ name: 'Medium', users: 5,  price: 500, },
		{ name: 'Large',  users: 10, price: 700, },
	];
	const users = [];
	for(let b=0; b<bands.length; b++){
		for(let u=users.length+1; u<=bands[b].users; u++){
			users.push({
				band: bands[b].name,
				price: bands[b].price,
				numUsers: u,
				userPrice: Math.round(bands[b].price / u),
			});
		}
	}
	const maxUsers = users.length;
	let numUsers = 1;
	$: details = users[numUsers-1];
</script>

<style>
	h3, h4, p {
		text-align: center;
	}
	input {
		margin: 0;
		width: 50%
	}
	.pricing {
		display: flex;
		margin: 20px -5px;
	}
	.pricing > div {
		flex: 1;
		background: #e7eaec;
		margin: 0 5px;
		padding: 10px;
		border: 3px solid #e7eaec;
		transition: all 300ms ease-in-out;
		z-index: 1;
  	box-shadow: 0 1px 3px rgba(0,0,0,0.12), 0 1px 2px rgba(0,0,0,0.24);
	}
	.pricing > div.active {
		transform: scale(1.1);
		z-index: 100;
		border-color: #1272d6;
  	box-shadow: 0 14px 28px rgba(0,0,0,0.25), 0 10px 10px rgba(0,0,0,0.22);
	}
</style>

<div class="pricing">
	{#each bands as { name, users, price }}
		<div class:active="{name === details.band}">
			<h3>{ name }</h3>
			<h4>{ users } Users</h4>
			<p>£ { price } / Month</p>
		</div>
	{/each}
</div>

<h3>
	<label>
		<input type=range bind:value={numUsers} min=1 max={maxUsers}>
	</label>
	{numUsers} users
</h3>

<h4>£ {details.userPrice} / User / Month</h4>
