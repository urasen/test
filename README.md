<!DOCTYPE html>
<html>
<head>
	<title>勤怠管理bot</title>
</head>
<body>
	<h1>勤怠管理bot</h1>

	<form>
		<label for="name">名前:</label>
		<input type="text" id="name" name="name"><br>

		<label for="date">日付:</label>
		<input type="date" id="date" name="date"><br>

		<label for="start">出勤時間:</label>
		<input type="time" id="start" name="start"><br>

		<label for="end">退勤時間:</label>
		<input type="time" id="end" name="end"><br>

		<input type="button" value="登録" onclick="addRecord()">
	</form>

	<table>
		<tr>
			<th>名前</th>
			<th>日付</th>
			<th>出勤時間</th>
			<th>退勤時間</th>
			<th>勤務時間</th>
		</tr>
	</table>

	<script>
		let records = [];

		function addRecord() {
			let name = document.getElementById("name").value;
			let date = document.getElementById("date").value;
			let start = document.getElementById("start").value;
			let end = document.getElementById("end").value;

			let record = {
				name: name,
				date: date,
				start: start,
				end: end
			};

			records.push(record);
			displayRecords();
		}

		function displayRecords() {
			let table = document.querySelector("table");

			for (let i = table.rows.length - 1; i > 0; i--) {
				table.deleteRow(i);
			}

			for (let i = 0; i < records.length; i++) {
				let row = table.insertRow(-1);
				let nameCell = row.insertCell(0);
				let dateCell = row.insertCell(1);
				let startCell = row.insertCell(2);
				let endCell = row.insertCell(3);
				let durationCell = row.insertCell(4);

				nameCell.innerHTML = records[i].name;
				dateCell.innerHTML = records[i].date;
				startCell.innerHTML = records[i].start;
				endCell.innerHTML = records[i].end;

				let start_time = new Date(records[i].date + "T" + records[i].start);
				let end_time = new Date(records[i].date + "T" + records[i].end);
				let duration = (end_time.getTime() - start_time.getTime()) / (1000 *
			60 * 60);

			durationCell.innerHTML = formatDuration(duration);
		}
	}

	function formatDuration(duration) {
		let hours = Math.floor(duration / 3600);
		let minutes = Math.floor((duration % 3600) / 60);

		return hours + "時間" + minutes + "分";
	}
</script>
</body>
</html>

