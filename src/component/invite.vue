<template>
  <div class="invite">
    <div class="inviteSvg">
      <svg
        v-if="isSvgView && randSvg === 1"
        class="ribbon"
        viewBox="0 0 400 400"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M179.981 276.772C164.375 267.266 161.18 262.061 147.634 248.36C66.1022 165.898 137.157 112.457 172.866 125.376C179.595 127.81 187.269 135.311 195.888 147.877C198.083 137.546 204.354 129.251 214.702 122.992C286.701 79.4431 320.679 175.189 251.306 237.353C234.603 252.325 207.881 277.281 196.844 287.597"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
      </svg>
      <svg
        v-if="isSvgView && randSvg === 2"
        class="ribbon"
        viewBox="0 0 500 500"
        xmlns="http://www.w3.org/2000/svg"
      >
        <g>
          <g>
            <g>
              <path
                d="M162.507,188.784c-1.579,0-3.129-0.64-4.25-1.75c-1.109-1.12-1.75-2.67-1.75-4.25c0-1.579,0.641-3.12,1.75-4.239
				c1.121-1.121,2.671-1.761,4.25-1.761c1.58,0,3.121,0.64,4.24,1.761c1.121,1.119,1.76,2.66,1.76,4.239
				c0,1.58-0.639,3.13-1.76,4.25C165.629,188.144,164.088,188.784,162.507,188.784z"
              />
            </g>
            <g>
              <path
                d="M271.675,86.465c-2.182-14.298-12.582-25.683-25.877-28.33c-10.348-2.062-20.346,1.516-27.93,9.671
				c-7.585-8.156-17.583-11.733-27.928-9.671c-13.297,2.647-23.696,14.032-25.877,28.331c-1.734,11.365-0.243,40.814,50.932,68.731
				c0.912,0.498,1.897,0.734,2.868,0.734l0.005-0.021l0.006,0.021c0.971,0,1.955-0.236,2.867-0.734
				C271.918,127.281,273.41,97.831,271.675,86.465z M217.869,143.06c-29.041-16.566-44.671-36.903-41.943-54.785
				"
              />
              <g>
                <g>
                  <path
                    d="M273.228,188.784c-1.58,0-3.131-0.64-4.24-1.75c-1.119-1.12-1.76-2.67-1.76-4.25c0-1.579,0.641-3.12,1.76-4.239
						c1.109-1.121,2.66-1.761,4.24-1.761c1.58,0,3.131,0.64,4.24,1.761c1.119,1.119,1.76,2.66,1.76,4.239
						c0,1.58-0.641,3.13-1.76,4.25C276.359,188.144,274.808,188.784,273.228,188.784z"
                  />
                </g>
                <path
                  d="M434.998,250.783c-0.828-1.508-2.264-2.588-3.941-2.967l-78.504-17.68c4.799-21.016-0.633-37.34-6.377-47.664
					c-8.336-14.984-22.746-26.658-37.605-30.467c-8.34-2.138-15.559-3.177-22.065-3.177c-15.047,0-24.51,5.655-34.531,11.642
					c-0.932,0.557-1.879,1.123-2.848,1.695l-31.258,7.207l-31.256-7.207c-0.97-0.572-1.918-1.139-2.85-1.695
					c-10.021-5.987-19.485-11.642-34.53-11.642c-6.507,0-13.725,1.039-22.066,3.177c-14.859,3.809-29.27,15.482-37.606,30.467
					c-5.744,10.324-11.176,26.648-6.376,47.664l-78.504,17.68c-1.678,0.379-3.113,1.459-3.94,2.967
					c-0.828,1.508-0.969,3.299-0.388,4.918c0.203,0.561,5.089,13.928,17.014,27.48c14.6,16.592,33.447,26.254,54.795,28.17
					c-0.836,6.363-4.614,18.871-20.125,34.563c-1.686,1.705-2.191,4.25-1.29,6.473c0.901,2.223,3.042,3.693,5.438,3.744
					c0,0,0.369,0.008,1.074,0.008c5.824,0,40.8-0.597,75.638-14.009c1.889,3.354,3.788,11.39-5.468,26.983
					c-1.691,2.85-0.752,6.529,2.098,8.223c0.96,0.568,2.015,0.84,3.057,0.84c2.048,0,4.043-1.049,5.165-2.938
					c11.246-18.944,9.661-30.979,6.223-37.833c5.498-2.596,10.909-5.555,16.122-8.917c3.551,5.328,8.163,17.253-1.268,36.947
					c-1.431,2.99-0.169,6.572,2.82,8.004c0.836,0.4,1.718,0.59,2.587,0.59c2.238,0,4.385-1.258,5.416-3.41
					c12.004-25.068,5.59-41.259,0.186-49.112c6.427-5.118,12.383-10.983,17.591-17.724c21.23-27.479,26.455-64.135,15.549-108.995
					l14.896-11.643l14.895,11.643c-10.906,44.86-5.684,81.517,15.547,108.995c5.207,6.739,11.161,12.602,17.587,17.72
					c-5.4,7.855-11.81,24.053,0.19,49.116c1.031,2.152,3.178,3.41,5.416,3.41c0.869,0,1.75-0.19,2.586-0.59
					c2.99-1.432,4.252-5.014,2.822-8.004c-9.433-19.696-4.818-31.619-1.268-36.946c5.212,3.362,10.623,6.32,16.119,8.916
					c-3.439,6.852-5.022,18.889,6.225,37.833c1.121,1.889,3.117,2.938,5.164,2.938c1.041,0,2.098-0.271,3.057-0.842
					c2.85-1.691,3.789-5.371,2.098-8.221c-9.292-15.654-7.44-23.608-5.477-26.986c34.841,13.414,69.821,14.012,75.645,14.012
					c0.002,0,0.004,0,0.006,0c0.701,0,1.068-0.008,1.068-0.008c2.398-0.051,4.539-1.521,5.44-3.744
					c0.9-2.223,0.396-4.768-1.291-6.473c-15.508-15.691-19.287-28.199-20.123-34.563c21.348-1.916,40.195-11.578,54.795-28.17
					c11.926-13.553,16.811-26.92,17.014-27.48C435.966,254.081,435.824,252.29,434.998,250.783z M192.506,187.738
					"
                />
              </g>
            </g>
          </g>
        </g>
      </svg>
      <svg
        v-if="isSvgView && randSvg === 3"
        class="ribbon"
        viewBox="0 0 500 500"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M208.8 178.494C210.706 234.424 143.341 287.589 168.352 345.317"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M209.54 171.025C200.69 169.12 191.801 166.306 183.739 162.043C175.313 157.591 167.19 154.266 160.354 147.348C100.32 86.5497 241.204 137.438 220.423 164.494"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M175.813 85.052C177.757 79.1751 180.649 72.4313 187.845 71.5608C196.483 70.5197 191.731 75.8778 194.444 79.804C195.136 80.8096 196.924 77.1676 197.546 76.8088C202.673 73.8383 208.569 72.6019 214.624 73.4368C220.844 74.2931 218.897 88.2676 216.567 91.4192C193.089 123.149 160.289 88.527 160.289 107.533"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M225.957 76.4089C240.893 99.8657 209.306 120.736 214.377 146.126"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M181.451 56.6314C155.79 40.8821 134.114 100.525 140.138 111.267"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M133.478 123.717C97.63 152.166 162.832 178.009 186.433 175.882"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M210.086 60.8933C221.796 54.0607 234.751 50.8839 247.371 58.1089C278.792 76.1016 226.296 126.771 226.296 153.596"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M253.621 106.288C290.246 128 250.934 152.499 228.76 159.82"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M197.638 239.497C218.463 211.413 273.887 228.707 291.009 204.638"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M175.226 248.211C160.142 239.912 134.305 239.539 116.714 242.24"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M152.865 238.472C97.4105 199.697 88.4057 287.205 154.063 245.233"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M227.66 219.97C239.791 195.509 267.959 199.979 289.703 199.979C290.692 199.979 279.138 209.32 273.03 218.768C259.623 239.502 248.142 249.431 223.78 231.161"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
      </svg>
      <svg
        v-if="isSvgView && randSvg === 4"
        class="ribbon"
        viewBox="0 0 400 400"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M108.443 195.261C109.389 188.19 129.163 157.263 131.631 155.824C138.942 151.559 241.296 154.88 255.301 163.374C260.802 166.71 282.111 207.172 282.111 212.076C282.111 215.174 230.068 217.677 221.06 218.126C210.664 218.645 188.064 217.202 165.413 212.076C146.852 207.874 128.679 202.079 109.389 199.843C108.931 199.789 120.253 218.666 131.631 235.002C136.938 242.625 173.01 311.215 178.003 313.469C182.995 315.723 271.407 220.682 282.963 212.463"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M220.27 219.771C208.261 245.315 186.688 294.075 182.994 308.692"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="12"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M168.311 218.554C172.106 248.613 177.256 278.838 180.736 308.692"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="12"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M176.217 151.559C169.16 171.543 171.251 194.109 168.311 214.899"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="12"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M216.882 156.431C218.828 174.48 216.357 207.792 222.53 219.771"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="12"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          opacity="0.503384"
          d="M176.218 155.213C165.329 168.694 145.594 191.59 142.331 202.718"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          opacity="0.503384"
          d="M134.423 160.085C136.047 172.618 141.424 184.297 143.459 196.628"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          opacity="0.503384"
          d="M179.606 156.431C194.584 173.96 194.867 195.198 210.105 212.463"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          opacity="0.503384"
          d="M210.106 163.739C199.122 178.66 185.918 191.779 176.219 207.59"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          opacity="0.503384"
          d="M227.05 161.304C246.433 176.191 260.44 194.917 276.751 211.245"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          opacity="0.503384"
          d="M77.2089 151.558C69.1045 146.077 61.9508 140.819 61 140.596"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          opacity="0.503384"
          d="M128.774 105.271C125.479 98.7234 128.774 99.6093 123.432 90.4736"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          opacity="0.503384"
          d="M212.404 111.362C211.098 103.438 212.417 94.8484 212.887 87"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          opacity="0.503384"
          d="M276.749 129.633C282.962 124.761 284.738 122.517 289.174 119.889"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          opacity="0.503384"
          d="M327.58 201.5C333.228 199.978 335.123 200.293 338.876 198.455"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          opacity="0.503384"
          d="M298.213 292.856C301.111 295.821 303.546 299.314 306.12 302.601"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          opacity="0.503384"
          d="M66.6479 230.118C65.098 231.955 62.8739 232.569 61 233.787"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          opacity="0.503384"
          d="M251.898 219.771L195.984 294.565"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
      </svg>
      <svg
        v-if="isSvgView && randSvg === 5"
        class="ribbon"
        viewBox="0 0 400 400"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M223.529 192.283C269.173 108.594 120 76.2002 120 172.31C120 186.631 125.493 201.693 136.449 209.629"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M176.105 94.0337C217.634 27.3505 309.474 92.4931 272.348 155.735C268.506 162.279 265.233 169.063 256.218 170.679"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M260.183 335C264.776 317.997 267.298 300.41 269.663 282.839C271.734 267.456 280.027 214.167 270.19 201.989C251.745 179.156 132.197 202.128 132.197 226.102C132.197 239.391 132.716 250.112 144.753 250.112C195.128 250.112 239.114 232.243 249.649 244.761C260.183 257.28 240.958 282.839 194.026 282.839"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M150.492 257.1C149.895 283.65 139.283 309.136 133.417 335"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          opacity="0.991676"
          d="M195.002 113.471C207.863 127.104 211.045 138.452 204.546 147.514C194.799 161.108 176.106 176.432 176.106 192.588"
          stroke="#000000"
          stroke-opacity="0.9"
          stroke-width="16"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
      </svg>
    </div>
    <div class="text">
      서로 다른 추억속에서 살아온<br />
      경기도 남자와 부산 여자가 만나, <br />
      이제는 같은 방향을 바라보며 함께 걸어가려합니다. <br />
      무엇이 다른지를 궁금해하던 연인에서 <br />
      서로의 다름마저 이해하고 사랑하는 부부가 되려합니다.<br /><br />
      저희 두 사람이 함께하는 새로운 시작에 <br />
      귀한 발걸음으로 축복해 주시면 감사하겠습니다.
    </div>
    <br /><br />
    <div><b>신랑 윤승현 · 신부 김민조</b></div>
  </div>
</template>
<script setup>
import { onMounted, ref } from "vue";
const isSvgView = ref(false);
const randSvg = ref(Math.floor(Math.random() * 5) + 1);
onMounted(() => {
  const callback = ([entry], observer) => {
    // console.log(entry.isIntersecting);
    isSvgView.value = entry.isIntersecting;
  };
  const observer = new IntersectionObserver(callback, null);
  const boxes = document.querySelector(".inviteSvg");
  // console.log(boxes);
  observer.observe(boxes);
});
</script>
<style lang="scss" scoped>
.invite {
  margin: 100px 0px;
}
.text {
  display: flex;
  flex-direction: column;
  line-height: 2;
}
.image {
  width: 70px;
  height: 70px;
  filter: opacity(0.8) drop-shadow(0 0 0 rgb(245, 5, 5));
}

.ribbon {
  width: 80px;
  overflow: visible;
}

.ribbon path {
  fill: none;
  stroke: var(--accent-color);
  stroke-width: 8;

  stroke-linecap: round;
  stroke-linejoin: round;

  stroke-dasharray: 2500;
  stroke-dashoffset: 2500;

  animation: draw 5s ease forwards;
}

@keyframes draw {
  to {
    stroke-dashoffset: 0;
  }
}
</style>
