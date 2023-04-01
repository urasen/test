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
      <label for="vacation_time">休暇時間:</label>
      <input type="number" id="vacation_time" name="vacation_time" min="0"><br><br>
      <input type="button" value="登録" onclick="saveData()">
    </form>
    <h2>登録済みデータ</h2>
    <table id="data_table">
      <tr>
        <th>名前</th>
        <th>日付</th>
        <th>出勤時刻</th>
        <th>退勤時刻</th>
        <th>休暇時間</th>
      </tr>
    </table>
    <script>
      function saveData() {
        // 入力された値を取得
        var name = document.getElementById("name").value;
        var date = document.getElementById("date").value;
        var start_time = document.getElementById("start_time").value;
        var end_time = document.getElementById("end_time").value;
        var vacation_time = document.getElementById("vacation_time").value;

        // 入力された値をオブジェクトにまとめる
        var data = {
          name: name,
          date: date,
          start_time: start_time,
          end_time: end_time,
          vacation_time: vacation_time
        };

        // 保存済みデータを取得
        var saved_data = localStorage.getItem("saved_data");
        if (saved_data) {
          // 保存済みデータがあれば、JSON形式からオブジェクトに変換する
          saved_data = JSON.parse(saved_data);
        } else {
          // 保存済みデータがなければ、空の配列を用意する
          saved_data = [];
        }

        // 入力されたデータを保存済みデータに追加する
        saved_data.push(data);

        // 保存済みデータをJSON形式に変換して、ローカルストレージに保存する
       
        var saved_data_json = JSON.stringify(saved_data);
        localStorage.setItem("saved_data", saved_data_json);

        // テーブルに登録済みデータを表示する
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
        vacation_time_cell.innerHTML = vacation_time;
      }

      // ページが読み込まれたときに保存済みデータをテーブルに表示する
      window.onload = function() {
        var saved_data = localStorage.getItem("saved_data");
        if (saved_data) {
          saved_data = JSON.parse(saved_data);
          var table = document.getElementById("data_table");
          for (var i = 0; i < saved_data.length; i++) {
            var data = saved_data[i];
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
          }
        }
      };
    </script>
  </body>
</html>
