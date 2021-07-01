<script>
	import firebase from 'firebase/app';  
	import "firebase/database";
	
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
		var f_name,keys=[],data,test = [];
            var final_data = [];
			var ref = firebase.database().ref("staff/-MdVIBNiWjQDq_yOfjve");
			ref.on("value", function(snapshot) {
			f_name = snapshot.val();
			for (const [key] of Object.entries(f_name)) {
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
</script>
<section>
        {#each final_data as f}
			<span>{f.f_name}</span><br>
		{/each}
</section>
