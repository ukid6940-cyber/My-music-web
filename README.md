
<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Music Player</title>
    <style>
        body {
            margin: 0;
            background-color: #0b0b0b;
            color: white;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
        }

        .player-card {
            width: 350px;
            text-align: center;
            padding: 20px;
        }

        .album-art {
            width: 100%;
            border-radius: 20px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
            margin-bottom: 30px;
        }

        .song-info h2 { margin: 0; font-size: 24px; }
        .song-info p { color: #b3b3b3; margin: 5px 0 25px 0; }

        .progress-container {
            width: 100%;
            height: 5px;
            background: #333;
            border-radius: 5px;
            cursor: pointer;
            margin-bottom: 10px;
        }

        .progress-bar {
            width: 0%;
            height: 100%;
            background: #fff;
            border-radius: 5px;
        }

        .time {
            display: flex;
            justify-content: space-between;
            font-size: 12px;
            color: #b3b3b3;
            margin-bottom: 20px;
        }

        .controls {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .btn-play {
            background: white;
            color: black;
            border: none;
            border-radius: 50%;
            width: 60px;
            height: 60px;
            font-size: 20px;
            cursor: pointer;
        }

        .btn-side {
            background: none;
            border: none;
            color: white;
            font-size: 24px;
            cursor: pointer;
        }
    </style>
</head>
<body>

<div class="player-card">
    <img src="9d7c8e35365963f4a6fa225cc9ad835d.jpg" alt="Album Art" class="album-art">

    <div class="song-info">
        <h2>SALAHKAH KITA</h2> <p>Robinhood</p>
    </div>

    <div class="progress-container" id="progress-container">
        <div class="progress-bar" id="progress-bar"></div>
    </div>
    <div class="time">
        <span id="current-time">0:00</span>
        <span id="duration">0:00</span>
    </div>

    <div class="controls">
        <button class="btn-side">shuffle</button>
        <button class="btn-side">⏮</button>
        <button class="btn-play" id="play-btn">▶</button>
        <button class="btn-side">⏭</button>
        <button class="btn-side">repeat</button>
    </div>

    <audio id="audio" src="RobinHood feat Asmirandah - Salahkah Kita.mp3"></audio>
</div>

<script>
    const audio = document.getElementById('audio');
    const playBtn = document.getElementById('play-btn');
    const progressBar = document.getElementById('progress-bar');
    const progressContainer = document.getElementById('progress-container');
    const currentTimeEl = document.getElementById('current-time');
    const durationEl = document.getElementById('duration');

    let isPlaying = false;

    function togglePlay() {
        if (isPlaying) {
            audio.pause();
            playBtn.innerText = '▶';
        } else {
            audio.play();
            playBtn.innerText = '⏸';
        }
        isPlaying = !isPlaying;
    }

    playBtn.addEventListener('click', togglePlay);

    audio.addEventListener('timeupdate', (e) => {
        const { duration, currentTime } = e.srcElement;
        const progressPercent = (currentTime / duration) * 100;
        progressBar.style.width = `${progressPercent}%`;

        // Hitung waktu
        let curMins = Math.floor(currentTime / 60);
        let curSecs = Math.floor(currentTime % 60);
        if (curSecs < 10) curSecs = `0${curSecs}`;
        currentTimeEl.innerText = `${curMins}:${curSecs}`;
        
        if(duration) {
            let durMins = Math.floor(duration / 60);
            let durSecs = Math.floor(duration % 60);
            if (durSecs < 10) durSecs = `0${durSecs}`;
            durationEl.innerText = `${durMins}:${durSecs}`;
        }
    });
</script>

</body>
</html>
