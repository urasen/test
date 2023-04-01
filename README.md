<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
    <title>勤怠管理システム</title>
  </head>
  <body>
    <h1>勤怠管理システム</h1>
    <form>
      <label for="name">社員名：</label>
      <input type="text" id="name" name="name" /><br />

      <label for="date">日付：</label>
      <input type="date" id="date" name="date" /><br />

      <label for="start_time">出勤時間：</label>
      <input type="time" id="start_time" name="start_time" /><br />

      <label for="end_time">退勤時間：</label>
      <input type="time" id="end_time" name="end_time" /><br />

      <label for="reason">休暇理由：</label>
      <input type="text" id="reason" name="reason" /><br />

      <button type="button" onclick="addData()">登録する</button>
    </form>

    <script>
      // スプレッドシートのIDを設定する
      var SPREADSHEET_ID = "スプレッドシートのID";

      function addData() {
        var name = document.getElementById("name").value;
        var date = document.getElementById("date").value;
        var start_time = document.getElementById("start_time").value;
        var end_time = document.getElementById("end_time").value;
        var reason = document.getElementById("reason").value;

        // スプレッドシートにデータを追加する関数を呼び出す
        google.script.run.addDataToSheet(name, date, start_time, end_time, reason, SPREADSHEET_ID);
      }
    </script>
  </body>
</html>
