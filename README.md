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
      <input type="button" value="CSVダウンロード" onclick="downloadCSV()">
      <input type="button" value="データリセット" onclick="resetData()">
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
          // 保存済みデータがなければ、空の配列を作成する
          saved_data = [];
        }

        // 新しいデータを追加する
        saved_data.push(data);

        // 更新されたデータを保存する
        localStorage.setItem("saved_data", JSON.stringify(saved_data));

        // テーブルに反映する
        updateTable();
      }

      function updateTable() {
        // 保存済みデータを取得
        var saved_data = localStorage.getItem("saved_data");
    // 保存済みデータを更新する
    var updated_data = false;
    for (var i = 0; i < saved_data.length; i++) {
      var saved_item = saved_data[i];
      if (saved_item.name == name && saved_item.date == date) {
        saved_item.start_time = start_time;
        saved_item.end_time = end_time;
        saved_item.vacation_time = vacation_time;
        updated_data = true;
        break;
      }
    }
    if (!updated_data) {
      // 新しいデータを追加する
      saved_data.push(data);
    }

    // データをローカルストレージに保存する
    localStorage.setItem("saved_data", JSON.stringify(saved_data));

    // テーブルにデータを表示する
    displayData();
  }

  function downloadCSV() {
    // 保存済みデータを取得
    var saved_data = localStorage.getItem("saved_data");
    if (saved_data) {
      // CSV形式に変換する
      var csv_data = "名前,日付,出勤時刻,退勤時刻,休暇時間\n";
      saved_data = JSON.parse(saved_data);
      for (var i = 0; i < saved_data.length; i++) {
        var item = saved_data[i];
        csv_data += item.name + "," + item.date + "," + item.start_time + "," + item.end_time + "," + item.vacation_time + "\n";
      }

      // ダウンロード用のリンクを作成する
      var blob = new Blob([csv_data], {type: "text/csv;charset=utf-8;"});
      var link = document.createElement("a");
      var url = URL.createObjectURL(blob);
      link.setAttribute("href", url);
      link.setAttribute("download", "data.csv");
      link.style.visibility = "hidden";
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
    } else {
      alert("データがありません。");
    }
  }

  function resetData() {
    // ローカルストレージからデータを削除する
    localStorage.removeItem("saved_data");

    // テーブルをクリアする
    var table = document.getElementById("data_table");
    var rows = table.rows;
    for (var i = rows.length - 1; i > 0; i--) {
      table.deleteRow(i);
    }
  }

  function displayData() {
    // 保存済みデータを取得してテーブルに表示する
    var saved_data = localStorage.getItem("saved_data");
    if (saved_data) {
      saved_data = JSON.parse(saved_data);
      var table = document.getElementById("data_table");
      var rows = table.rows;
      // すでに表示されているデータをクリアする
      for (var i = rows.length - 1; i > 0; i--) {
        table.deleteRow(i);
      }
      // データを表示する
      for (var i = 0; i < saved_data.length; i++) {
        var item = saved_data[i];
        var row = table.insertRow();
        row.insertCell().textContent = item.name;
        row.insertCell().textContent = item.date;
        row.insertCell().textContent = item.start_time;
        row
    }

    // データを保存する
    localStorage.setItem("saved_data", JSON.stringify(saved_data));

    // テーブルに行を追加する
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

  function downloadCSV() {
    // 保存済みデータを取得
    var saved_data = localStorage.getItem("saved_data");
    if (saved_data) {
      // 保存済みデータがあれば、JSON形式からオブジェクトに変換する
      saved_data = JSON.parse(saved_data);
      // CSV形式の文字列を作成する
      var csv_data = "名前,日付,出勤時刻,退勤時刻,休暇時間\n";
      for (var i = 0; i < saved_data.length; i++) {
        csv_data += saved_data[i].name + "," +
                    saved_data[i].date + "," +
                    saved_data[i].start_time + "," +
                    saved_data[i].end_time + "," +
                    saved_data[i].vacation_time + "\n";
      }
      // ダウンロード用のリンクを作成する
      var link = document.createElement("a");
      link.href = "data:text/csv;charset=utf-8," + encodeURIComponent(csv_data);
      link.download = "data.csv";
      document.body.appendChild(link);
      link.click();
      document.body.removeChild(link);
    } else {
      alert("保存されたデータがありません。");
    }
  }

  function resetData() {
    // 保存されたデータを削除する
    localStorage.removeItem("saved_data");

    // テーブルの行を削除する
    var table = document.getElementById("data_table");
    var rows = table.rows.length;
    for (var i = 1; i < rows; i++) {
      table.deleteRow(1);
    }
  }

</script>
  </body>
</html>
