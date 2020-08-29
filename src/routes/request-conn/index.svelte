<script>
	import { goto, stores } from '@sapper/app';
	import ListErrors from '../_components/ListErrors.svelte';
	import RequestconnectionForm from './_request-conn.svelte';
	import * as api from 'api.js';

	let inProgress;
	let errors;
	let user = { };
	let mentor = { };
	let mentorskills = { };
	const { session, page } = stores();

	 async function save(event) {
	// 	inProgress = true;
	// 	const response = await post(`auth/save`, event.detail);
	// 	errors = response.errors;
	// 	if (response.user) $session.user = response.user;
	// 	inProgress = false;
	 }

	async function getData() {
		console.log($session);
		let token = $session.user.access_token;
		user = await api.get('users/8', token);
		mentor = await api.get('users/6', token);
		mentorskills = mentor.Skills;
		//console.log(user);
		console.log(mentor.Skills);
		// console.log(mentor.Skills[0].UserSkills.skilltype);
		// console.log(mentor.Skills[0].skillname);
		// {skillname: "C#", UserSkills: {…}} skilltype: "guide"}
	}
	getData();

</script>

<svelte:head>
	<title>Request</title>
</svelte:head>

<div class="settings-page">
	<div class="container page">
		<div class="row">
			<div class="col-md-6 offset-md-3 col-xs-12">

				<h1 class="text-xs-center">request Connection</h1>

				<ListErrors {errors}/>
				<RequestconnectionForm on:save={save} {inProgress} user={user} mentor = {mentor} mentorskills = {mentorskills}/>
			</div>
		</div>
	</div>
</div>