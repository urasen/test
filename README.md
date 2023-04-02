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
      // 登録済みデータの配列
      var data_array = [];

      // データを保存する
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

        // データを配列に追加
        data_array.push(data);

        // テーブルにデータを表示する
        displayData();

        // 入力フォームをクリアする
        clearForm();
      }

      // データを表示する
      function displayData() {
        // テーブルのtbodyを取得
        var tbody = document.getElementById("data_table").getElementsByTagName("tbody")[0];

        // tbodyを初期化する
        tbody.innerHTML = "";

       // データをテーブルに表示する
      for (var i = 0; i < data_array.length; i++) {
      var data = data_array[i];
      var row = tbody.insertRow(-1);
      var nameCell = row.insertCell(0);
      var dateCell = row.insertCell(1);
      var startTimeCell = row.insertCell(2);
      var endTimeCell = row.insertCell(3);
      var vacationTimeCell = row.insertCell(4);
      nameCell.innerHTML = data.name;
      dateCell.innerHTML = data.date;
      startTimeCell.innerHTML = data.start_time;
      endTimeCell.innerHTML = data.end_time;
      vacationTimeCell.innerHTML = data.vacation_time;
      }
    }
  // 入力フォームをクリアする
  function clearForm() {
    document.getElementById("name").value = "";
    document.getElementById("date").value = "";
    document.getElementById("start_time").value = "";
    document.getElementById("end_time").value = "";
    document.getElementById("vacation_time").value = "";
  }

  // データをCSV形式でダウンロードする
  function downloadCSV() {
    // ヘッダー行を作成
    var csv = "名前,日付,出勤時刻,退勤時刻,休暇時間\n";

    // データ行を作成
    for (var i = 0; i < data_array.length; i++) {
      var data = data_array[i];
      csv += data.name + "," + data.date + "," + data.start_time + "," + data.end_time + "," + data.vacation_time + "\n";
    }

    // CSVファイルを作成
    var blob = new Blob([csv], { type: "text/csv" });
    var url = URL.createObjectURL(blob);
    var a = document.createElement("a");
    a.download = "data.csv";
    a.href = url;
    a.click();
  }

  // データをリセットする
  function resetData() {
    // 配列を初期化する
    data_array = [];

    // テーブルを初期化する
    var tbody = document.getElementById("data_table").getElementsByTagName("tbody")[0];
    tbody.innerHTML = "";
  }
</script>
 </body>
</html>                                            
