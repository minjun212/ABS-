<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>공 추적 스트라이크 판정</title>
  <style>
    video, canvas { position: absolute; width: 100%; height: 100%; }
  </style>
</head>
<body>
  <video id="cam_input" autoplay playsinline></video>
  <canvas id="output"></canvas>
  <script async src="https://docs.opencv.org/4.x/opencv.js"></script>
  <script>
    let video = document.getElementById("cam_input");
    let canvas = document.getElementById("output");
    let ctx = canvas.getContext("2d");

    navigator.mediaDevices.getUserMedia({video: { facingMode: "environment" }, audio: false})
     .then(스트림 => video.srcObject = 스트림);

    함수 크기 조정Canvas() {
     캔버스.너비 = 창.내부 너비;
     캔버스.높이 = 창.내부 높이;
    }
    window.onresize = resizeCanvas;
    캔버스 크기 조정();

    스트리밍 = false를 허용합니다;
    video.addEventListener('재생 중', () => {
     만약 (!streaming) {
     스트리밍 = true;
     processVideo();
     }
    });

    함수 프로세스Video() {
     만약 (cv === '정의되지 않음'의 유형) {
     요청 애니메이션 프레임(프로세스 비디오);
     반환;
     }

     캡 = new cv.비디오 캡처(비디오);
     src = new cv.매트(비디오).높이, 비디오.너비, CV.CV_8UC4);
     hsv = new cv.매트();
     마스크 = new cv.매트();
      let contours = new cv.MatVector();
      let hierarchy = new cv.Mat();

      const STRIKEZONE = {
        x: video.width / 2 - 60,
        y: video.height / 2 - 100,
        w: 120,
        h: 200
      };

      function loop() {
        cap.read(src);
        cv.cvtColor(src, hsv, cv.COLOR_RGBA2RGB);
        cv.cvtColor(hsv, hsv, cv.COLOR_RGB2HSV);

     낮게 = 새로 cv.Mat(hsv.rows, hsv.cols, hsv.type(), [20, 100, 100, 0]); // 노란색 하한
     높음 = 새 CV를 놓습니다.Mat(hsv.rows, hsv.cols, hsv.type(), [30, 255, 255, 255]); // 노란색 상한
     cv.inRange(hsv, 낮음, 높음, 마스크);

     cv.findContours(마스크, 윤곽선, 계층 구조, cv).RET_외부, CV.체인_APREX_SIMPLE);
     중심 = null을 두십시오;
     (i = 0, i < contournes.size (); ++i) {에 대해
     cnt = contours.get(i);
     면적 = cv.contourArea(cnt);
     만약 (면적 > 500) {
     모멘트 = cv.moments(cnt);
     cx = moments.m10 / moments.m00이라고 합니다;
     cy = moments.m01 / moments.m00;
     center = { x: cx, y: cy };
     }
     }

     // 그리기
<!DOCTYPE HTML>
        ctx.strokeStyle = "white";
<머리>
 <meta charset="utf-8">
 <title>공 추적 스트라이크 판정</title>
 <스타일>
 비디오, 캔버스 {위치: 절대; 너비: 100%; 높이: 100%; }
 </스타일>
</머리>
<바디>
 <video id="cam_input" 자동 재생 인라인></video>
 <canvas id="출력"></canvas>
 <script async src="https://docs.opencv.org/4.x/opencv.js "></script>
 <스크립트>
 video = document.getElementById("cam_input")를 허용합니다;
 canvas = document.getElementById("출력")을 허용합니다;
 ctx = canvas.getContext("2d")를 지정합니다;

 navigator.mediaDevices.getUserMedia({비디오: {facingMode: {facingMode: "환경" }, 오디오: false})
 .then(스트림 => video.srcObject = 스트림);
      loop();
 함수 크기 조정Canvas() {
 캔버스.너비 = 창.내부 너비;
 캔버스.높이 = 창.내부 높이;
 }
 window.onresize = resizeCanvas;
