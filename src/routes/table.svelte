<script>
	import firebase from 'firebase/app';  
	import "firebase/database";
	import { onMount } from 'svelte';
	var Config = {
			apiKey: "AIzaSyB89muKEyIeXS-1cleyTE3I5r-4es-7xZk",
			authDomain: "sveltefire-5ad20.firebaseapp.com",
			projectId: "sveltefire-5ad20",
			storageBucket: "sveltefire-5ad20.appspot.com",
			messagingSenderId: "683389184470",
			appId: "1:683389184470:web:dfb309f291f64d232a1c77",
			measurementId: "G-030BTP2GFK"
		};
		if (!firebase.apps.length) {
			firebase.initializeApp(Config);
		}else {
			firebase.app(); // if already initialized, use that one
		}
		var keys=[],data,test = [],final_data = [];
		onMount(() => {
			var ref = firebase.database().ref("staff/-MdVIBNiWjQDq_yOfjve");
			ref.on("value", function(snapshot) {
			var test_key = snapshot.val();
			for (const [key] of Object.entries(test_key)) {
				keys.push(`${key}`);
			}
			for(let i in keys){
				var refer = firebase.database().ref("staff/-MdVIBNiWjQDq_yOfjve/"+ keys[i] +"");
				refer.on("value", function(snapshot){
					data = snapshot.val();
					final_data.push(data);
					test = [];
				});
			}
			console.log(final_data);
			}, function (error) {
			console.log("Error: " + error.code);
			});
		});
		
</script>
<section>
	<table class="ml-96 mt-20 bg-green-100 font-bold">
		<thead>
			<tr>
				<td class="border border-green-700 px-6 py-1">Name</td>
				<td class="border border-green-700 px-6 py-1">Age</td>
				<td class="border border-green-700 px-6 py-1">Position</td>
				<td class="border border-green-700 px-6 py-1">Office</td>
				<td class="border border-green-700 px-6 py-1">Joined</td>
			</tr>
		</thead>
	</table>
</section>
