<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>20/10</title>
    <link rel="stylesheet" href="style.css">
</head>
<body> 
    <audio  autoplay>
        <source src="./y2mate.com - Chloe Adams  Prettys On The Inside Nightcore.mp3" type="audio/mp3">
    </audio>

   
    
</body>
</html>

@import url('https://fonts.googleapis.com/css?family=Indie+Flower');
@import url('https://fonts.googleapis.com/css2?family=Dancing+Script:wght@400..700&family=Edu+AU+VIC+WA+NT+Guides:wght@400..700&family=Merriweather:ital,wght@0,300;0,400;0,700;0,900;1,300;1,400;1,700;1,900&family=Moon+Dance&display=swap');
@import url('https://fonts.googleapis.com/css?family=Amatic+SC');
body {
  	/* background: #84bcea;  */
	margin: 0px;
	padding: 0px;
	font-weight: bold;
	background: url("https://images.rawpixel.com/image_800/czNmcy1wcml2YXRlL3Jhd3BpeGVsX2ltYWdlcy93ZWJzaXRlX2NvbnRlbnQvbHIvcGRmZW1pbmluZTEtMjBiLW5hcC5qcGc.jpg");
	/* background-image: 10000px; */
}

::selection {
	background: transparent;
}

h4 {
	font-size: 26px;
	line-height: 1px;
	font-family: "Dancing Script", cursive !important;
}

.color1{color:#bc1b4e}/*MOUNTAIN MEADOW*/
.color2{color:#C0392B/*TALL POPPY*/}


.card {
	color: #013243; /*SHERPA BLUE*/
	position: absolute;
	top: 50%;
	left: 50%;
	width: 400px;
	height: 550px;
	background: #f8d8e3;
	transform-style: preserve-3d;
	transform: translate(-50%,-50%) perspective(2000px);
	box-shadow: inset 300px 0 50px rgba(0,0,0,.5), 20px 0 60px rgba(0,0,0,.5);
	transition: 1s;
}

.card:hover {
	transform: translate(-50%,-50%) perspective(2000px) rotate(15deg) scale(1.2);
	box-shadow: inset 20px 0 50px rgba(0,0,0,.5), 0 10px 100px rgba(0,0,0,.5);
}

.card:before {
	content:'';
	position: absolute;
	top: -5px;
	left: 0;
	width: 100%;
	height: 5px;
	background: #f8d8e3;
	transform-origin: bottom;
	transform: skewX(-35deg);
}

.card:after {
	content: '';
	position: absolute;
	top: 0;
	right: -5px;
	width: 5px;
	height: 100%;
	background: #f8d8e3;
	transform-origin: left;
	transform: skewY(-35deg);
}

.card .imgBox {
	width: 100%;
	height: 100%;
	position: relative;
	transform-origin: left;
	transition: .7s;
}

.card .bark {
	position: absolute;
	background: #f8d8e3;
	width: 100%;
	height: 100%;
	opacity: 0;
	transition: .7s;
}

.card .imgBox img {
	min-width: 400px;
	max-height: 550px;
}

.card:hover .imgBox {
	transform: rotateY(-135deg);
}

.card:hover .bark {
	opacity: 1;
	transition: .6s;
  box-shadow: 300px 200px 100px rgba(0, 0, 0, .4) inset;
}

.card .details {
	position: absolute;
	top: 0;
	left: 0;
	box-sizing: border-box;
	/* padding: 0 0 0 10px; */
	z-index: -1;
	/* margin-top: 70px; */
}

.card .details .wish p {
	font-size: 15px;
	/* line-height: 5px; */
	/* padding: 5px 20px; */
	text-align: justify;
	/* margin: 15px 0px; */
}

.wish{
	/* margin: 10px 20px; */
	text-align: justify;
	font-family: "Dancing Script", cursive;
	font-size: 30px;
}

.card .details .wish img{
	height: 550px;
	width: 400px;
}

// Import the data to customize and insert them into page
const fetchData = () => {
  fetch("customize.json")
    .then(response => response.json())
    .then(data => {
      const dataArr = Object.keys(data);
      dataArr.map(customData => {
        if (data[customData] !== "") {
          const element = document.querySelector(`[data-node-name*="${customData}"]`);
          if (customData === "imagePath") {
            element.setAttribute("src", data[customData]);
          } else {
            element.innerText = data[customData];
          }
        }

        // Check if the iteration is over
        // Run animation if so
        if (dataArr.length === dataArr.indexOf(customData) + 1) {
          animationTimeline();
        } 
      });
    })
    .catch(error => console.error("Error fetching data:", error)); // Thêm phần bắt lỗi
};

// Animation Timeline
const animationTimeline = () => {
  // Split chars that need to be animated individually
  const textBoxChars = document.getElementsByClassName("hbd-chatbox")[0];
  const hbd = document.getElementsByClassName("wish-hbd")[0];

  textBoxChars.innerHTML = `<span>${textBoxChars.innerHTML.split("").join("</span><span>")}</span>`;
  hbd.innerHTML = `<span>${hbd.innerHTML.split("").join("</span><span>")}</span>`;

  const ideaTextTrans = {
    opacity: 0,
    y: -20,
    rotationX: 5,
    skewX: "5deg" // Giảm độ nghiêng
  };

  const ideaTextTransLeave = {
    opacity: 0,
    y: 20,
    rotationY: 5,
    skewX: "5deg" // Giảm độ nghiêng
  };

  const tl = new TimelineMax();

  tl
    .to(".container", 0.1, {
      visibility: "visible"
    })
    .from(".one", 0.7, {
      opacity: 0,
      y: 10
    })
    .from(".two", 0.4, {
      opacity: 0,
      y: 10
    })
    .to(
      ".one",
      0.7,
      {
        opacity: 0,
        y: 10
      },
      "+=2.5"
    )
    .to(
      ".two",
      0.7,
      {
        opacity: 0,
        y: 10
      },
      "-=1"
    )
    .from(".three", 0.7, {
      opacity: 0,
      y: 10
    })
    .to(
      ".three",
      0.7,
      {
        opacity: 0,
        y: 10
      },
      "+=2"
    )
    .from(".four", 0.7, {
      scale: 0.2,
      opacity: 0
    })
    .from(".fake-btn", 0.3, {
      scale: 0.2,
      opacity: 0
    })
    .staggerTo(
      ".hbd-chatbox span",
      0.5,
      {
        visibility: "visible"
      },
      0.05
    )
    .to(".fake-btn", 0.1, {
      backgroundColor: "rgb(127, 206, 248)"
    })
    .to(
      ".four",
      0.5,
      {
        scale: 0.2,
        opacity: 0,
        y: -150
      },
      "+=0.7"
    )
    .from(".idea-1", 0.7, ideaTextTrans)
    .to(".idea-1", 0.7, ideaTextTransLeave, "+=1.5")
    .from(".idea-2", 0.7, ideaTextTrans)
    .to(".idea-2", 0.7, ideaTextTransLeave, "+=1.5")
    .from(".idea-3", 0.7, ideaTextTrans)
    .to(".idea-3 strong", 0.5, {
      scale: 1.2,
      x: 10,
      backgroundColor: "rgb(21, 161, 237)",
      color: "#fff"
    })
    .to(".idea-3", 0.7, ideaTextTransLeave, "+=1.5")
    .from(".idea-4", 0.7, ideaTextTrans)
    .to(".idea-4", 0.7, ideaTextTransLeave, "+=1.5")
    .from(
      ".idea-5",
      0.7,
      {
        rotationX: 15,
        rotationZ: -10,
        skewY: "0deg", // Đặt lại skewY về 0
        y: 50,
        z: 10,
        opacity: 0
      },
      "+=0.5"
    )
    .to(
      ".idea-5 .smiley",
      0.7,
      {
        rotation: 90,
        x: 8
      },
      "+=0.4"
    )
    .to(
      ".idea-5",
      0.7,
      {
        scale: 0.2,
        opacity: 0
      },
      "+=2"
    )
    .staggerFrom(
      ".idea-6 span",
      0.8,
      {
        scale: 3,
        opacity: 0,
        rotation: 15,
        ease: Expo.easeOut
      },
      0.2
    )
    .staggerTo(
      ".idea-6 span",
      0.8,
      {
        scale: 3,
        opacity: 0,
        rotation: -15,
        ease: Expo.easeOut
      },
      0.2,
      "+=1"
    )
    .staggerFromTo(
      ".baloons img",
      2.5,
      {
        opacity: 0.9,
        y: 1400
      },
      {
        opacity: 1,
        y: -1000
      },
      0.2
    )
    .from(
      ".lydia-dp",
      0.5,
      {
        scale: 3.5,
        opacity: 0,
        x: 25,
        y: -25,
        rotationZ: -45
      },
      "-=2"
    )
    .from(".hat", 0.5, {
      x: -100,
      y: 350,
      rotation: -180,
      opacity: 0
    })
    .staggerFrom(
      ".wish-hbd span",
      0.7,
      {
        opacity: 0,
        y: -50,
        rotation: 150,
        skewX: "1deg", // Giảm độ nghiêng
        ease: Elastic.easeOut.config(1, 0.5)
      },
      0.1
    )
    .staggerFromTo(
      ".wish-hbd span",
      0.7,
      {
        scale: 1.4,
        rotationY: 150
      },
      {
        scale: 1,
        rotationY: 0,
        color: "#ff69b4",
        ease: Expo.easeOut
      },
      0.1,
      "party"
    )
    .from(
      ".wish h5",
      0.5,
      {
        opacity: 0,
        y: 10,
        skewX: "-1deg" // Giảm độ nghiêng
      },
      "party"
    )
    .staggerTo(
      ".eight svg",
      1.5,
      {
        visibility: "visible",
        opacity: 0,
        scale: 80,
        repeat: 3,
        repeatDelay: 1.4
      },
      0.3
    )
    .to(".six", 0.5, {
      opacity: 0,
      y: 30,
      zIndex: "-1"
    })
    .staggerFrom(".nine p", 1, ideaTextTrans, 1.2)
    .to(
      ".last-smile",
      0.5,
      {
        rotation: 90
      },
      "+=1"
    );

  // Restart Animation on click
  const replyBtn = document.getElementById("replay");
  replyBtn.addEventListener("click", () => {
    tl.restart();
  });
};

// Run fetch and animation in sequence
fetchData();

