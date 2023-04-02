<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>勤怠管理システム</title>
  </head>
  <body>
    <h1>勤怠管理システム</h1>
    <form>
      <label for="name">名前:</label>
      <input type="text" id="name" name="name"><br><br>
      <label for="date">日付:</label>
      <input type="date" id="date" name="date"><br><br>
      <label for="start_time">出勤時刻:</label>
      <input type="time" id="start_time" name="start_time"><br><br>
      <label for="end_time">退勤時刻:</label>
      <input type="time" id="end_time" name="end_time"><br><br>
      <label for="vacation_time_hours">休暇時間(時間):</label>
      <input type="number" id="vacation_time_hours" name="vacation_time_hours" min="0"><br><br>
      <label for="vacation_time_minutes">休暇時間(分):</label>
      <input type="number" id="vacation_time_minutes" name="vacation_time_minutes" min="0" max="59"><br><br>
      <input type="button" value="登録" onclick="saveData()">
    </form>
    <h2>登録済みデータ</h2>
    <table id="data_table">
      <tr>
        <th>名前</th>
        <th>日付</th>
        <th>出勤時刻</th>
        <th>退勤時刻</th>
        <th>休暇時間(分)</th>
      </tr>
    </table>
    <br>
    <input type="button" value="CSV出力" onclick="exportCSV()">
    <input type="button" value="リセット" onclick="resetData()">
    <script>
      function saveData() {
        // 入力された値を取得
        var name = document.getElementById("name").value;
        var date = document.getElementById("date").value;
        var start_time = document.getElementById("start_time").value;
        var end_time = document.getElementById("end_time").value;
        var vacation_time_hours = document.getElementById("vacation_time_hours").value;
        var vacation_time_minutes = document.getElementById("vacation_time_minutes").value;

        // 入力された値をオブジェクトにまとめる
        var data = {
          name: name,
          date: date,
          start_time: start_time,
          end_time: end_time,
          vacation_time: vacation_time_hours * 60 + parseInt(vacation_time_minutes)
        };

        // 保存済みデータを取得
        var saved_data = localStorage.getItem("saved_data");
        if (saved_data) {
          // 保存済みデータがあれ
if (saved_data) {
saved_data = JSON.parse(saved_data);
} else {
saved_data = [];
}
      
          // 新しいデータを追加
    saved_data.push(data);

    // データを保存
    localStorage.setItem("saved_data", JSON.stringify(saved_data));

    // テーブルにデータを追加
    var table = document.getElementById("data_table");
    var row = table.insertRow(-1);
    var name_cell = row.insertCell(0);
    var date_cell = row.insertCell(1);
    var start_time_cell = row.insertCell(2);
    var end_time_cell = row.insertCell(3);
    var vacation_time_cell = row.insertCell(4);
    name_cell.innerHTML = name;
    date_cell.innerHTML = date;
    start_time_cell.innerHTML = start_time;
    end_time_cell.innerHTML = end_time;
    vacation_time_cell.innerHTML = vacation_time_hours * 60 + parseInt(vacation_time_minutes);
  }

  function exportCSV() {
    // 保存済みデータを取得
    var saved_data = localStorage.getItem("saved_data");
    if (saved_data) {
      saved_data = JSON.parse(saved_data);
    } else {
      saved_data = [];
    }

    // CSV形式に変換
    var csv = "名前,日付,出勤時刻,退勤時刻,休暇時間(分)\n";
    saved_data.forEach(function(data) {
      csv += data.name + "," + data.date + "," + data.start_time + "," + data.end_time + "," + data.vacation_time + "\n";
    });

    // ダウンロード
    var blob = new Blob([csv], {type: "text/csv"});
    var link = document.createElement("a");
    link.href = URL.createObjectURL(blob);
    link.download = "data.csv";
    link.click();
  }

  function resetData() {
    // 確認ダイアログを表示し、OKならデータをリセット
    if (confirm("登録したデータをすべて削除します。よろしいですか？")) {
      localStorage.removeItem("saved_data");
      location.reload();
    }
  }

  // 初期表示時に保存済みデータをテーブルに表示
  var saved_data = localStorage.getItem("saved_data");
  if (saved_data) {
    saved_data = JSON.parse(saved_data);
    var table = document.getElementById("data_table");
    saved_data.forEach(function(data) {
      var row = table.insertRow(-1);
      var name_cell = row.insertCell(0);
      var date_cell = row.insertCell(1);
      var start_time_cell = row.insertCell(2);
      var end_time_cell = row.insertCell(3);
      var vacation_time_cell = row.insertCell(4);
      name_cell.innerHTML = data.name;
      date_cell.innerHTML = data.date;
      start_time_cell.innerHTML = data.start_time;
      end_time_cell.innerHTML = data.end_time;
      vacation_time_cell.innerHTML = data.vacation_time;
    });
  }
</script>
</body>
</html>
      
