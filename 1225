











var face_colors = "fec5bb-fcd5ce-fae1dd-f8edeb-e8e8e4-d8e2dc-ece4db-ffe5d9-ffd7ba-fec89a".split("-").map(a => "#" + a);
var eye_colors = "323031-3d3b3c-7f7979-c1bdb3-5f5b6b".split("-").map(a => "#" + a);
var pos_x = [];
var pos_y = [];
var sizes = [];
var colors = [];
var v_y = [];
var txts;
var face_move_var = false;
var lang = navigator.language;
var myRec = new p5.SpeechRec(lang);
var face_Rot_var = false;


var soundChristmas; // 聖誕音樂播放器的變數
var soundChillVibes; // 冷靜音樂播放器的變數


function preload() {
  soundChristmas = loadSound('alex-productions-christmas-magic.mp3');
  soundChillVibes = loadSound('alex-productions-chill-vibes.mp3');
}


function setup() {
  createCanvas(windowWidth, windowHeight);


  inputElement = createInput("412730508范翔宇");
  inputElement.position(10, 10);
  inputElement.size(140, 40);
  inputElement.style("font-size", "20px");
  inputElement.style("color", " #00DB00");
  inputElement.style("background", "#E6E6F2");
  inputElement.style("border", "1");


  btnmoveElement = createButton("移動");
  btnmoveElement.position(170, 10);
  btnmoveElement.size(80, 40);
  btnmoveElement.style("font-size", "20px");
  btnmoveElement.style("color", "#000000");
  btnmoveElement.style("background", "#E6E6F2");
  btnmoveElement.style("border", "1");
  btnmoveElement.mousePressed(face_move);


  btnStopElement = createButton("暫停");
  btnStopElement.position(270, 10);
  btnStopElement.size(80, 40);
  btnStopElement.style("font-size", "20px");
  btnStopElement.style("color", "#000000");
  btnStopElement.style("background", "#E6E6F2");
  btnStopElement.style("border", "1");
  btnStopElement.mousePressed(face_stop);


  btnvoiceElement = createButton("語音");
  btnvoiceElement.position(470, 10);
  btnvoiceElement.size(80, 40);
  btnvoiceElement.style("font-size", "20px");
  btnvoiceElement.style("color", "#000000");
  btnvoiceElement.style("background", "#E6E6F2");
  btnvoiceElement.style("border", "1");
  btnvoiceElement.mousePressed(voice_go);


  radioElement = createRadio();
  radioElement.option("暫停");
  radioElement.option("旋轉");
  radioElement.option("移動");
  radioElement.position(370, 10);
  radioElement.size(80, 40);
  radioElement.style("font-size", "20px");
  radioElement.style("color", "#000");
  radioElement.style("background", "#f3d5");


  // 創建切換音樂的按鈕
  toggleMusicBtn = createButton("切換音樂");
  toggleMusicBtn.position(570, 10);
  toggleMusicBtn.size(120, 40);
  toggleMusicBtn.style("font-size", "20px");
  toggleMusicBtn.style("color", "#000000");
  toggleMusicBtn.style("background", "#E6E6F2");
  toggleMusicBtn.style("border", "1");
  toggleMusicBtn.mousePressed(toggleMusic);
}


function draw() {
  background("#b8d4e3");
  let mode = radioElement.value();
  for (var i = 0; i < pos_x.length; i++) {
    push();
    txts = inputElement.value();
    translate(pos_x[i], pos_y[i]);


    // 獲取音樂振幅大小
    let level = soundChillVibes ? soundChillVibes.getLevel() * 5 : 1;


    // 將音樂振幅大小應用到文本圖案大小
    let adjustedSize = sizes[i] * level;
    scale(adjustedSize);


    // 眼睛跟著滑鼠移動
    let eyeX = map(mouseX, 0, width, -25, 25);
    let eyeY = map(mouseY, 0, height, -15, 15);


    if (mode == "旋轉") {
      rotate(sin(frameCount / 10 * v_y[i]));
    } else {
      if (mode == "移動") {
        face_move_var = false;
      }
    }
    drawCustomFace(txts, colors[i], eye_colors[0], eyeX, eyeY);
    pop();
    if (face_move_var || mode == "移動") {
      pos_y[i] = pos_y[i] + v_y[i];
    }
    if (pos_y[i] > height || pos_y[i] < 0) {
      pos_x.splice(i, 1);
      pos_y.splice(i, 1);
      sizes.splice(i, 1);
      colors.splice(i, 1);
      v_y.splice(i, 1);
    }
  }
}


function drawCustomFace(txts, face_clr, eye_clr, eyeX, eyeY) {
  fill(255, 192, 203);
  textSize(50);
  text(txts, 50, 200);
  fill(face_clr);


  // legs
  rect(125, 250, 25, 125);
  rect(250, 250, 25, 125);
  fill(0);
  rect(125, 350, 25, 25);
  rect(250, 350, 25, 25);


  fill(255, 192, 203);


  // body
  ellipse(200, 200, 250, 200);


  // ears
  ellipse(165, 150, 25, 50);
  ellipse(235, 150, 25, 50);


  // face
  circle(200, 200, 125);


  // left eye
  fill(255);
  circle(175 + eyeX, 170 + eyeY, 25);
  fill(0);
  circle(175 + eyeX, 170 + eyeY, 10);


  // right eye
  fill(255);
  circle(225 + eyeX, 170 + eyeY, 25);
  fill(0);
  circle(225 + eyeX, 170 + eyeY, 10);


  // nose
  fill(255, 192, 203);
  ellipse(200, 210, 50, 25);
  fill(0);
  circle(190, 210, 10);
  circle(210, 210, 10);


  // mouth
  noFill();
  arc(200, 225, 50, 50, PI * 0.25, PI * 0.75);
}


function mousePressed() {
  if (mouseY > 60) {
    pos_x.push(mouseX);
    pos_y.push(mouseY);
    sizes.push(random(0.3, 1));
    colors.push(face_colors[int(random(face_colors.length))]);
    v_y.push(random(-1, 1));
  }
}


function face_move() {
  face_move_var = true;
}


function face_stop() {
  face_move_var = false;
}


function voice_go() {
  myRec.onResult = showResult;
  myRec.start();
}


function showResult() {
  if (myRec.resultValue == true) {
    print(myRec.resultString);
    let lowStr = myRec.resultString.toLowerCase();
    let mostrecentword = lowStr.sp;
    if (myRec.resultString.indexOf("走") !== -1) {
      face_move_var = true;
    }
    if (myRec.resultString.indexOf("停") !== -1) {
      face_move_var = false;
      face_Rot_var = false;
    }
  }
}


function toggleMusic() {
  if (radioElement.value() === '旋轉') {
    // 如果是旋轉模式，切換到 chill vibes 音樂
    if (soundChillVibes.isPlaying()) {
      soundChillVibes.pause();
    } else {
      soundChillVibes.loop();
    }
  } else {
    // 否則切換到 christmas magic 音樂
    if (soundChristmas.isPlaying()) {
      soundChristmas.pause();
    } else {
      soundChristmas.loop();
    }
  }
}





