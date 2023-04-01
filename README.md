<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>勤怠管理システム</title>
  <script src="https://code.jquery.com/jquery-3.5.1.min.js"></script>
  <script>
    $(function() {
      $('#submit').on('click', function() {
        var name = $('#name').val();
        var date = $('#date').val();
        var start_time = $('#start_time').val();
        var end_time = $('#end_time').val();
        var vacation_time = $('#vacation_time').val();

        var row = [name, date, start_time, end_time, vacation_time];
        google.script.run.recordAttendance(row);
        alert('勤怠情報を記録しました。');
        $('#name').val('');
        $('#date').val('');
        $('#start_time').val('');
        $('#end_time').val('');
        $('#vacation_time').val('');
      });
    });
  </script>
</head>
<body>
  <h1>勤怠管理システム</h1>
  <form>
    <label>名前：</label><input type="text" id="name"><br>
    <label>日付：</label><input type="date" id="date"><br>
    <label>出勤時間：</label><input type="time" id="start_time"><br>
    <label>退勤時間：</label><input type="time" id="end_time"><br>
    <label>休暇時間：</label><input type="number" id="vacation_time" value="0"><br>
    <input type="button" id="submit" value="送信">
  </form>
</body>
</html>
