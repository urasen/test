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
<!DOCTYPE html>
<html>
<head>
	<title>勤怠管理システム</title>
</head>
<body>
	<h1>勤怠管理システム</h1>
	<p>社員名：</p>
	<input type="text" id="employee-name">
	<br><br>
	<p>出勤時間を入力してください：</p>
	<input type="time" id="start-time">
	<br><br>
	<p>退勤時間を入力してください：</p>
	<input type="time" id="end-time">
	<br><br>
	<p>休暇申請：</p>
	<select id="vacation-request">
		<option value="none">なし</option>
		<option value="am">午前休</option>
		<option value="pm">午後休</option>
		<option value="all">全休</option>
	</select>
	<br><br>
	<button onclick="recordAttendance()">勤怠を記録する</button>
	<br><br>
	<p>社員名：</p>
	<span id="employee-name-display"></span>
	<br><br>
	<p>労働時間：</p>
	<span id="work-time"></span>
	<br><br>
	<p>休暇申請：</p>
	<span id="vacation-request-display"></span>

	<script>
		function recordAttendance() {
			var employeeName = document.getElementById("employee-name").value;
			var startTime = document.getElementById("start-time").value;
			var endTime = document.getElementById("end-time").value;
			var vacationRequest = document.getElementById("vacation-request").value;

			var start = new Date("2023-04-02T" + startTime + ":00");
			var end = new Date("2023-04-02T" + endTime + ":00");

			var diff = end.getTime() - start.getTime();
			var hours = Math.floor(diff / (1000 * 60 * 60));
			var minutes = Math.floor((diff % (1000 * 60 * 60)) / (1000 * 60));

			var workTime = hours + "時間" + minutes + "分";
			document.getElementById("employee-name-display").innerHTML = employeeName;
			document.getElementById("work-time").innerHTML = workTime;
			document.getElementById("vacation-request-display").innerHTML = vacationRequest;
		}
	</script>
</body>
</html>
