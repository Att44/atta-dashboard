<script>
    import supabase from '$lib/db';
import { each } from 'svelte/internal';

    async function logout() {
   	 const { error } = await supabase.auth.signOut();

   	 if (error) alert(error.message); // alert if error
    }

// 	let timetable = {
// 	Monday: [],
// 	Tuesday: [],
// 	Wednesday: [],
// 	Thursday: [],
// 	Friday: [],
//   };

  let timetable = {
    Monday: [
      {
        name: "PH",
        period: 1,
        style: "",
      },
      {
        name: "PM",
        period: 1,
        style: "",
      },
      {
        name: "BI",
        period: 2,
        style: "",
      },
      {
        name: "R",
        period: 1,
        style: "table-success",
      },
      {
        name: "BM",
        period: 2,
        style: "",
      },
      {
        name: "M3",
        period: 2,
        style: "",
      },
      {
        name: "BC",
        period: 2,
        style: "",
      },
	  ],
    Tuesday: [
  	{
    	name: "PJPK",
    	period: 1,
    	style: "",
  	},
  	{
    	name: "M3",
    	period: 2,
    	style: "",
  	},
  	{
    	name: "BI",
    	period: 1,
    	style: "",
  	},
  	{
    	name: "E",
    	period: 1,
    	style: "table-success",
  	},
  	{
    	name: "BM",
    	period: 2,
    	style: "",
  	},
  	{
    	name: "BC",
    	period: 3,
    	style: "",
  	},
  	{
    	name: "PJPK",
    	period: 1,
    	style: "",
  	},
	],
	Wednesday: [
  	{
    	name: "BC",
    	period: 3,
    	style: "",
  	},
  	{
    	name: "PM",
    	period: 1,
    	style: "",
  	},
  	{
    	name: "H",
    	period: 1,
    	style: "table-success",
  	},
  	{
    	name: "PKS",
    	period: 3,
    	style: "",
  	},
  	{
    	name: "BM",
    	period: 2,
    	style: "",
  	},
	],
	Thursday: [
  	{
    	name: "SA",
    	period: 1,
    	style: "",
  	},
  	{
    	name: "PJPK",
    	period: 1,
    	style: "",
  	},
  	{
    	name: "BM",
    	period: 2,
    	style: "",
  	},
  	{
    	name: "A",
    	period: 1,
    	style: "table-success",
  	},
  	{
    	name: "PM",
    	period: 1,
    	style: "",
  	},
  	{
    	name: "BC",
    	period: 2,
    	style: "",
  	},
  	{
    	name: "M3",
    	period: 2,
    	style: "",
  	},
	],
	Friday: [
  	{
    	name: "BI",
    	period: 2,
    	style: "",
  	},
  	{
    	name: "BM",
    	period: 2,
    	style: "",
  	},
  	{
    	name: "T",
    	period: 1,
    	style: "table-success",
  	},
  	{
    	name: "BC",
    	period: 2,
    	style: "",
  	},
  	{
    	name: "PM",
    	period: 1,
    	style: "",
  	},
  	{
    	name: "SA",
    	period: 2,
    	style: "",
  	},
	],
  };

  function addTimeSlot(day){
	if (day === "Monday") {
  	timetable.Monday = [
    	...timetable.Monday,
    	{ name: "??", period: 1, style: "" },
  	];
	} else if (day === "Tuesday") {
  	timetable.Tuesday = [
    	...timetable.Tuesday,
    	{ name: "??", period: 1, style: "" },
  	];
	} else if (day === "Wednesday") {
  	timetable.Wednesday = [
    	...timetable.Wednesday,
    	{ name: "??", period: 1, style: "" },
  	];
	} else if (day === "Thursday") {
  	timetable.Thursday = [
    	...timetable.Thursday,
    	{ name: "??", period: 1, style: "" },
  	];
	} else if (day === "Friday") {
  	timetable.Friday = [
    	...timetable.Friday,
    	{ name: "??", period: 1, style: "" },
  	];
	}
  }

  let curDay;
  let curIndex;
  let curName;
  let curPeriod;
  let curStyle;

  function showCurData(day, index, name, period, style) {
	curDay = day;
	curIndex = index;
	curName = name;
	curPeriod = period;
	curStyle = style;
  }

  function deleteTimeSlot(day, index) {
	if (day === "Monday") {
		timetable.Monday.splice(index, 1);
		timetable = timetable;
	} else if (day === "Tuesday") {
		timetable.Tuesday.splice(index, 1);
		timetable = timetable;
	} else if (day === "Wednesday") {
		timetable.Wednesday.splice(index, 1);
		timetable = timetable;
	} else if (day === "Thursday") {
		timetable.Thursday.splice(index, 1);
		timetable = timetable;
	} else if (day === "Friday") {
		timetable.Friday.splice(index, 1);
		timetable = timetable;
	}
      saveEntry();
  }
  
  function setTimeSlot(day, index, newName, newPeriod, newStyle) {
	if (day === "Monday") {
		timetable.Monday[index].name = newName;
		timetable.Monday[index].period = newPeriod;
		timetable.Monday[index].style = newStyle;
	} else if (day === "Tuesday") {
		timetable.Tuesday[index].name = newName;
		timetable.Tuesday[index].period = newPeriod;
		timetable.Tuesday[index].style = newStyle;
	} else if (day === "Wednesday") {
		timetable.Wednesday[index].name = newName;
		timetable.Wednesday[index].period = newPeriod;
		timetable.Wednesday[index].style = newStyle;
	} else if (day === "Thursday") {
		timetable.Thursday[index].name = newName;
		timetable.Thursday[index].period = newPeriod;
		timetable.Thursday[index].style = newStyle;
	} else if (day === "Friday") {
		timetable.Friday[index].name = newName;
		timetable.Friday[index].period = newPeriod;
		timetable.Friday[index].style = newStyle;
	}
	saveEntry();
  }

  async function saveEntry() {
	const { error } = await supabase.from("studentEntries").upsert(
  	{
    	user_id: supabase.auth.user().id,
    	timetable: timetable,
  	},
  	{ onConflict: "user_id" }
	);
	if (error) alert(error.message);
  }

  // Get entries
  async function getEntries() {
	const { data, error } = await supabase.from("studentEntries").select();
	if (error) alert(error.message);

	if (data != "") {
  	timetable = data[0].timetable;
	}
  }

  getEntries();


</script>

<div class="container mt-5">
    <h1>My Dashboard</h1>
    <p>School Timetable</p>
    <table class="table table-bordered table-striped text-center caption-top">
        <thead class="table-success">
            <tr>
              <th scope="col">#</th>
              <th scope="col">1</th>
              <th scope="col">2</th>
              <th scope="col">3</th>
              <th scope="col">4</th>
              <th scope="col">-</th>
              <th scope="col">5</th>
              <th scope="col">6</th>
              <th scope="col">7</th>
              <th scope="col">8</th>
              <th scope="col">9</th>
              <th scope="col">10</th>
            </tr>
          </thead>
          <tbody>
            <tr >
              <th class="table-success" scope="row">MON</th>
              {#each timetable.Monday as timeSlot, index}
              <td colspan={timeSlot.period} class={timeSlot.style}>
                <button type="button" class="btn" data-bs-toggle="modal"data-bs-target="#editTimeSlot" on:click={() =>
					showCurData(
					  "Monday",
					  index,
					  timeSlot.name,
					  timeSlot.period,
					  timeSlot.style
					)}>
                  {timeSlot.name}
                </button>
              </td>
              {/each}
			  <td>
				<button class="btn" on:click={() => addTimeSlot("Monday")}>+</button>
			  </td>
            </tr>
            <tr>
              <th class="table-success" scope="row">TUE</th>
              {#each timetable.Tuesday as timeSlot, index}
              <td colspan={timeSlot.period} class={timeSlot.style}>
                <button type="button" class="btn" data-bs-toggle="modal"data-bs-target="#editTimeSlot" on:click={() =>
					showCurData(
					  "Tuesday",
					  index,
					  timeSlot.name,
					  timeSlot.period,
					  timeSlot.style
					)}>
                  {timeSlot.name}
                </button>
              </td>
              {/each}
			  <td>
				<button class="btn" on:click={() => addTimeSlot("Tuesday")}>+</button>
			  </td>
            </tr>
            <tr>
              <th class="table-success" scope="row">WED</th>
              {#each timetable.Wednesday as timeSlot, index}
              <td colspan={timeSlot.period} class={timeSlot.style}>
                <button type="button" class="btn" data-bs-toggle="modal"data-bs-target="#editTimeSlot" on:click={() =>
					showCurData(
					  "Wednesday",
					  index,
					  timeSlot.name,
					  timeSlot.period,
					  timeSlot.style
					)}>
                  {timeSlot.name}
                </button>
              </td>
              {/each}
			  <td>
				<button class="btn" on:click={() => addTimeSlot("Wednesday")}>+</button>
			  </td>
            </tr>
            <tr>
              <th class="table-success" scope="row">THU</th>
              {#each timetable.Thursday as timeSlot, index}
              <td colspan={timeSlot.period} class={timeSlot.style}>
                <button type="button" class="btn" data-bs-toggle="modal"data-bs-target="#editTimeSlot" on:click={() =>
					showCurData(
					  "Thursday",
					  index,
					  timeSlot.name,
					  timeSlot.period,
					  timeSlot.style
					)}>
                  {timeSlot.name}
                </button>
              </td>
              {/each}
			  <td>
				<button class="btn" on:click={() => addTimeSlot("Thursday")}>+</button>
			  </td>
            </tr>
            <tr>
              <th class="table-success" scope="row">FRI</th>
              {#each timetable.Friday as timeSlot, index}
              <td colspan={timeSlot.period} class={timeSlot.style}>
                <button type="button" class="btn" data-bs-toggle="modal"data-bs-target="#editTimeSlot" on:click={() =>
					showCurData(
					  "Friday",
					  index,
					  timeSlot.name,
					  timeSlot.period,
					  timeSlot.style
					)}>
                  {timeSlot.name}
                </button>
              </td>
              {/each}
			  <td>
				<button class="btn" on:click={() => addTimeSlot("Friday")}>+</button>
			  </td>
            </tr>
          </tbody>
    </table>

</div>

  
<!-- Modal -->
<div class="modal fade" id="editTimeSlot" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
<div class="modal-dialog">
	<div class="modal-content">
	<div class="modal-header">
		<h5 class="modal-title" id="exampleModalLabel">Edit Time Slot</h5>
		<button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
	</div>
	<div class="modal-body">
		<!-- Name input -->
		<div class="input-group mb-3">
			<span class="input-group-text" id="name" >Name</span>
			<input type="text" class="form-control" bind:value={curName} >
		</div>

		<!-- Period input -->
		<div class="input-group mb-3">
			<span class="input-group-text" id="period" >Period</span>
			<input type="number" class="form-control" bind:value={curPeriod} >
		</div>

		<!-- Style input -->
		<div class="input-group mb-3">
			<label class="input-group-text" for="inputGroupSelect01">Style</label>
			<select class="form-select" id="style" bind:value={curStyle}>
				<option value="">Default</option>
				<option value="table-primary">Blue</option>
				<option value="table-success">Green</option>
				<option value="table-danger">Red</option>
				<option value="table-warning">Yellow</option>
				<option value="table-secondary">Grey</option>
			</select>
			</div>

	</div>
	<div class="modal-footer">
		<button type="button" class="btn btn-secondary" data-bs-dismiss="modal"> 
			Cancel
		</button>
		<button type="button" on:click={() => deleteTimeSlot(curDay, curIndex)} class="btn btn-danger" data-bs-dismiss="modal">
			Delete
		</button>
		<button	type="button" on:click={() => setTimeSlot(curDay, curIndex, curName, curPeriod, curStyle)} class="btn btn-primary" data-bs-dismiss="modal">
			Save changes
		</button>
	</div>
	</div>
</div>
</div>


<!-- Sign Out -->
<section class="container px-4 py-3 text-center">
    <button class="btn btn-secondary" on:click={logout}>Logout</button>
</section>	