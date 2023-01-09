# Alarm-clock
my first repository
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="style.CSS">

    <title>alarm clock</title>
</head>

<body>
    <div id="clockContainer">
        <h1>Current Time</h1>
        <div id="CurrentTime">
        </div>
        <div id="alarmForm">
            <form onsubmit="event.preventDefault(); addAlarm();">

                <input id="alarm-hour" type="number" name="hour" min="0" max="12" placeholder="Enter hour" required>
                <input id="alarm-min" type="number" name="min" min="0" max="60" placeholder="Enter minutes" required>
                <select id="alarm-period" name="Time period " id="period">
                    <option value="PM">PM</option>
                    <option value="AM">AM</option>
                </select>
                <button id="btn1">Add Alarm</button>
            </form>
        </div>
        <section id="OurAlarm">
            <div id="AlarmName">

            </div>

        </section>
        <audio src="Alarm.mp3"></audio>
    </div>
    <script>
        const fakeAlarms = [
            { hour: 5, min: 50, period: 'am' },
            { hour: 6, min: 30, period: 'am' },
            { hour: 7, min: 15, period: 'am' }
        ];
        const deleteAlarm = () => {
        };
        const addAlarm = (data) => {
            const alarm = {};
            alarm.hour = parseInt(document.getElementById('alarm-hour').value);
            alarm.min = parseInt(document.getElementById('alarm-min').value);
            alarm.period = document.getElementById('alarm-period').value;
            fakeAlarms.push(alarm);
            renderAlarms();
        }
        const fireAlarm = () => {
            alert('alarm is working');
        }
        const renderTime = () => {
            var currentTime = document.getElementById("CurrentTime");
            const currentDate = new Date();
            var hours = currentDate.getHours();
            var minutes = currentDate.getMinutes();
            var seconds = currentDate.getSeconds();
            var TimePeriod = hours >= 12 ? "PM" : "AM";
            if (hours > 12) {
                hours = hours % 12;
            }
            if (fakeAlarms.find(({ hour, min, period }) => hour === hours && minutes === min && period === TimePeriod && seconds === 1)) {
                fireAlarm();
            }
            const timeString = getTimeString({ hours, minutes, seconds, TimePeriod });
            currentTime.innerHTML = timeString;
        };
        const getTimeString = ({ hours, minutes, seconds, TimePeriod }) => {
            if (minutes / 10 < 1) {
                minutes = "0" + minutes;
            }
            if (seconds / 10 < 1) {
                seconds = "0" + seconds;
            }
            return `${hours}:${minutes}:${seconds} ${TimePeriod}`;
        };
        setInterval(renderTime, 1000);
        //------------------------------------------------------------//

        function renderAlarm(alarm) {
            return (
                '<div class="alarm">' +
                '<span class="alarm-time">' + alarm.hour + ':' + alarm.min + ' ' + alarm.period + '</span>' + '</div>'
            );
        }
        const renderAlarms = () => {
            const alarmsSection = document.querySelector('#AlarmName');
            alarmsSection.innerHTML = '';
            let alarmsText = '';
            fakeAlarms.forEach((alarm) => {
                alarmsText += renderAlarm(alarm);
            });
            alarmsSection.innerHTML = alarmsText;
        };
        window.onload = function () {
            renderAlarms();
        }

    </script>
    <style>
        body {
            font-family: monaco;
            height: 100vh;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            background-color: #191515;
            font-family: 'Courier New', Courier, monospace;
        }

        #btn1 {
            display: flex;
            align-items: center;
            margin-left: auto;
            margin-right: auto;
            margin-top: 10px;
            background: none;
            color: #ffa260;
            border: 2px solid;
            padding: 1em 2em;
            font-size: 1em;
            transition: all 0.25s;
            border-radius: 5px;
            font-family: 'Courier New', Courier, monospace;
        }

        input,
        select {
            margin-top: 10px;
            width: 100px !important;
            text-align: center;
            margin-left: auto;
            margin-right: auto;
            font-family: 'Courier New', Courier, monospace;

        }



        h1 {
            font-family: 'Courier New', Courier, monospace;
            text-align: center;
            color: #ffa260;
        }

        #btn1:hover {
            border-color: #f1ff5c;
            color: white;
            box-shadow: 0 0.5em 0.5em -0.4em #f1ff5c;
            transform: translateY(-0.25em);
            cursor: pointer;
        }

        #CurrentTime {
            text-align: center;
            color: white;
            font-size: 50px;
        }

        #OurAlarm {
            padding-top: 10px;
            color: white;
            text-align: center;
        }
    </style>
</body>

</html>
