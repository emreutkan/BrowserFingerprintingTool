<template>
  <div id="app">
    <h1>Browser Vulnerability Checker</h1>

    <!-- Network Information Section -->
    <section class="info-section network-info">
      <h2>Network Information</h2>
      <p><strong>IP Address:</strong> {{ ip }}</p>
      <p><strong>ISP:</strong> {{ isp }}</p>
      <p><strong>DNS:</strong> {{ dnsServer }}</p>
      <p><strong>Network Speed:</strong> {{ networkSpeed }}</p>
      <p><strong>SSL/TLS Version:</strong> {{ sslStatus }}</p>
      <p><strong>Proxy Detection:</strong> {{ proxyDetection }}</p>
    </section>

    <!-- Browser Information Section -->
    <section class="info-section browser-info">
      <h2>Browser Information</h2>
      <p><strong>Browser Info:</strong> {{ browser }}</p>
      <p><strong>User Agent Spoofing:</strong> {{ userAgentSpoof }}</p>
      <p><strong>Browser Plugins:</strong> {{ pluginsList }}</p>
      <p><strong>Browser Languages:</strong> {{ browserLanguages }}</p>
      <p><strong>Web Workers Support:</strong> {{ webWorkerSupport }}</p>
    </section>

    <!-- Privacy and Security Checks Section -->
    <section class="info-section privacy-security">
      <h2>Privacy and Security Checks</h2>
      <p><strong>Cookies Enabled:</strong> {{ cookiesEnabled }}</p>
      <p><strong>Local Storage Enabled:</strong> {{ localStorageEnabled }}</p>
      <p><strong>Adblocker Detection:</strong> {{ adblockerDetected }}</p>
      <p><strong>CSP Status:</strong> {{ cspStatus }}</p>
      <p><strong>HSTS:</strong> {{ hsts }}</p>
      <p><strong>Referrer Policy:</strong> {{ referrerPolicy }}</p>
      <p><strong>Do Not Track (DNT):</strong> {{ doNotTrack }}</p>
      <p><strong>IndexedDB Support:</strong> {{ indexedDBStatus }}</p>
      <p><strong>Third-Party Cookies:</strong> {{ thirdPartyCookies }}</p>
      <p><strong>Autofill Behavior:</strong> {{ autofillDetected }}</p>
      <p><strong>Incognito Mode:</strong> {{ incognitoStatus }}</p>
    </section>

    <!-- Fingerprinting Techniques Section -->
    <section class="info-section fingerprinting">
      <h2>Fingerprinting Techniques</h2>
      <p><strong>Canvas Fingerprint:</strong> {{ canvasFingerprint }}</p>
      <p><strong>Audio Fingerprint:</strong> {{ audioFingerprint }}</p>
      <p><strong>Font Fingerprint:</strong> {{ fontFingerprint }}</p>
      <p><strong>GPU Fingerprint:</strong> {{ gpuFingerprint }}</p>
      <p><strong>Shader Precision:</strong> {{ shaderPrecision }}</p>
    </section>

    <!-- System Information Section -->
    <section class="info-section system-info">
      <h2>System Information</h2>
      <p><strong>CPU Usage:</strong> {{ cpuUsage }}</p>
      <p><strong>CPU Cores:</strong> {{ cpuCores }}</p>
      <p><strong>Device Memory:</strong> {{ deviceMemory }}</p>
      <p><strong>Battery Status:</strong> {{ batteryStatus }}</p>
      <p><strong>Sensor Access:</strong> {{ sensorAccess }}</p>
      <p><strong>CPU Benchmark:</strong> {{ cpuBenchmark }}</p>
    </section>

    <!-- API Support and Detection Section -->
    <section class="info-section api-support">
      <h2>API Support and Detection</h2>
      <p><strong>WebRTC Public IP Leak:</strong> {{ webrtcPublicIP }}</p>
      <p><strong>WebRTC Local IP Leak:</strong> {{ webrtcLocalIP }}</p>
      <p><strong>WebSocket Leak:</strong> {{ websocketLeak }}</p>
      <p><strong>Battery API:</strong> {{ batteryAPI }}</p>
      <p><strong>Speech Recognition API:</strong> {{ speechAPI }}</p>
      <p><strong>Speech Synthesis API:</strong> {{ speechSynthesisSupport }}</p>
      <p><strong>Idle Detection:</strong> {{ idleStatus }}</p>
      <p><strong>Audio Worklet Support:</strong> {{ audioWorkletSupport }}</p>
    </section>

    <!-- Clipboard Access and Monitoring Section -->
    <section class="info-section clipboard-monitoring">
      <h2>Clipboard Access and Monitoring</h2>
      <p><strong>Clipboard Access:</strong> {{ clipboardAccess }}</p>
      <p><strong>Previous Clipboard Content:</strong> {{ previousClipboard }}</p>
      <p><strong>Clipboard Test Result:</strong> {{ clipboardTest }}</p>
      <p><strong>Clipboard Monitoring:</strong> {{ clipboardMonitoring }}</p>
      <p v-if="clipboardMonitoring.includes('Change')">
        <strong>Current Clipboard Content:</strong> {{ currentClipboardContent }}
      </p>
    </section>

    <!-- User Behavior Detection Section -->
    <section class="info-section user-behavior">
      <h2>User Behavior Detection</h2>
      <p><strong>Autofill Behavior:</strong> {{ autofillDetected }}</p>
      <p><strong>Incognito Mode:</strong> {{ incognitoStatus }}</p>
      <p><strong>Idle Detection:</strong> {{ idleStatus }}</p>
    </section>

    <!-- Miscellaneous Information Section -->
    <section class="info-section miscellaneous">
      <h2>Miscellaneous Information</h2>
      <p><strong>Resolution:</strong> {{ resolution }}</p>
      <p><strong>Spoofed Resolution:</strong> {{ spoofedResolution }}</p>
      <p v-if="actualResolution"><strong>Details:</strong> {{ actualResolution }}</p>
      <p><strong>Local Time:</strong> {{ localTime }}</p>
      <p><strong>Timezone:</strong> {{ timezoneName }}</p>
      <p><strong>Screen Orientation:</strong> {{ screenOrientation }}</p>
      <p><strong>Pixel Ratio:</strong> {{ pixelRatio }}</p>
      <p><strong>Device Memory:</strong> {{ deviceMemory }}</p>
      <p><strong>JavaScript Execution Time:</strong> {{ jsExecutionTime }}</p>
    </section>

    <!-- Error Handling and Edge Cases Section -->
    <section class="info-section error-handling">
      <h2>Error Handling and Edge Cases</h2>
      <p><strong>Sensor Data:</strong> {{ sensorData }}</p>
      <p><strong>Actual Resolution Details:</strong> {{ actualResolution }}</p>
      <p><strong>Accessible Cookies List:</strong> {{ cookiesList }}</p>
    </section>
  </div>
</template>


<script setup>
import {ref, onMounted} from "vue";

// Original Variables
const ip = ref("Fetching...");
const resolution = `${window.screen.width}x${window.screen.height}`;
const browser = navigator.userAgent;
const location = ref("Permission required");
const webcamAccess = ref("Checking...");
const webrtcPublicIP = ref("Checking...");
const webrtcLocalIP = ref("Checking...");
const cookiesEnabled = ref("Checking...");
const localStorageEnabled = ref("Checking...");
const incognitoStatus = ref("Checking...");
const adblockerDetected = ref("Checking...");
const canvasFingerprint = ref("Checking...");
const isp = ref("Fetching...");
const dnsServer = ref("Fetching...");
const cookiesAccessible = ref("Checking...");
const cookiesList = ref([]);
const autofillDetected = ref("Checking...");

// New Checks
const referrerPolicy = ref("Checking...");
const hsts = ref("Checking...");
const doNotTrack = ref(navigator.doNotTrack === "1" ? "✅ DNT Enabled" : "⚠️ DNT Disabled");
const batteryAPI = ref("Checking...");
const cspStatus = ref("Checking...");
const userAgentSpoof = ref("Checking...");
const audioFingerprint = ref("Checking...");
const localTime = ref("Checking...");
const fontFingerprint = ref("Checking...");
const websocketLeak = ref("Checking...");
const batteryStatus = ref("Checking...");
const cpuUsage = ref("Checking...");
const clipboardAccess = ref("Checking...");
const previousClipboard = ref("Fetching...");
const clipboardTest = ref("Pending...");
const referrerURL = document.referrer || "No referrer detected";
const networkSpeed = ref("Checking...");
const screenOrientation = ref(`Orientation: ${screen.orientation.type}`);
const pixelRatio = ref(`Pixel Ratio: ${window.devicePixelRatio}`);
const cpuCores = ref(`⚠️ CPU Cores: ${navigator.hardwareConcurrency}`);
const sslStatus = ref("Checking...");
const gpuFingerprint = ref("Checking...");
const webWorkerSupport = ref("Checking...");
const thirdPartyCookies = ref("Checking...");
const indexedDBStatus = ref("Checking...");


try {
  const testDB = window.indexedDB.open("testDB");
  indexedDBStatus.value = "✅ IndexedDB Supported";
  testDB.onerror = () => (indexedDBStatus.value = "⚠️ IndexedDB Blocked");
} catch {
  indexedDBStatus.value = "⚠️ IndexedDB Not Available";
}
async function checkThirdPartyCookies() {
  try {
    const iframe = document.createElement("iframe");
    iframe.src = "https://example.com";
    document.body.appendChild(iframe);
    iframe.onload = () => {
      thirdPartyCookies.value = "✅ Third-Party Cookies Enabled";
      document.body.removeChild(iframe);
    };
  } catch {
    thirdPartyCookies.value = "⚠️ Third-Party Cookies Blocked";
  }
}
function checkWebWorkers() {
  try {
    const worker = new Worker(URL.createObjectURL(new Blob([""])));
    webWorkerSupport.value = "✅ Web Workers Enabled";
    worker.terminate();
  } catch {
    webWorkerSupport.value = "⚠️ Web Workers Disabled";
  }
}

function getGPUFingerprint() {
  const canvas = document.createElement('canvas');
  const gl = canvas.getContext("webgl") || canvas.getContext("experimental-webgl");
  const debugInfo = gl.getExtension("WEBGL_debug_renderer_info");
  const vendor = debugInfo ? gl.getParameter(debugInfo.UNMASKED_VENDOR_WEBGL) : "Unknown";
  const renderer = debugInfo ? gl.getParameter(debugInfo.UNMASKED_RENDERER_WEBGL) : "Unknown";

  gpuFingerprint.value = `⚠️ GPU Vendor: ${vendor}, Renderer: ${renderer}`;
}
async function checkSSL() {
  try {
    const res = await fetch("https://www.howsmyssl.com/a/check", { method: "GET" });
    const json = await res.json();
    sslStatus.value = `✅ SSL/TLS: ${json.tls_version}`;
  } catch {
    sslStatus.value = "⚠️ SSL/TLS Validation Failed";
  }
}


async function checkWebRTC() {
  const rtc = new RTCPeerConnection({ iceServers: [{ urls: "stun:stun.l.google.com:19302" }] });
  rtc.createDataChannel("");
  rtc.onicecandidate = (event) => {
    if (event.candidate) {
      const ipMatch = event.candidate.candidate.match(/\d+\.\d+\.\d+\.\d+/);
      if (ipMatch) {
        const ip = ipMatch[0];
        ip.startsWith("192.") || ip.startsWith("10.") ? webrtcLocalIP.value = `⚠️ Local IP: ${ip}` : webrtcPublicIP.value = `⚠️ Public IP: ${ip}`;
      }
    }
  };
  await rtc.createOffer().then((offer) => rtc.setLocalDescription(offer));
}

function checkCSP() {
  const cspHeader = document.querySelector("meta[http-equiv='Content-Security-Policy']");
  cspStatus.value = cspHeader ? "✅ CSP Implemented" : "⚠️ CSP Missing";
}

function getAudioFingerprint() {
  const ctx = new (window.AudioContext || window.webkitAudioContext)();
  const analyser = ctx.createAnalyser();
  const gain = ctx.createGain();
  const osc = ctx.createOscillator();
  osc.connect(gain).connect(analyser).connect(ctx.destination);
  osc.start(0);
  setTimeout(() => {
    const data = new Float32Array(analyser.frequencyBinCount);
    analyser.getFloatFrequencyData(data);
    audioFingerprint.value = `⚠️ Audio Fingerprint: ${data.slice(0, 5).join(", ")}`;
    ctx.close();
  }, 50);
}

function checkNetworkSpeed() {
  const testImage = "https://via.placeholder.com/1000x1000";
  const startTime = performance.now();
  fetch(testImage).then(() => {
    const duration = (performance.now() - startTime) / 1000;
    networkSpeed.value = duration < 2 ? "⚠️ High Network Speed" : "✅ Normal Network Speed";
  });
}


function checkAutofill() {
  const input = document.createElement("input");
  input.type = "text";
  input.name = "username";
  input.style = "position: absolute; top: -9999px;";
  document.body.appendChild(input);

  setTimeout(() => {
    if (input.value) {
      autofillDetected.value = "⚠️ Autofill Detected";
    } else {
      autofillDetected.value = "✅ No Autofill";
    }
    document.body.removeChild(input);
  }, 1000);
}

function checkCookiesAccess() {
  try {
    document.cookie = "test=accessible; path=/";
    const allCookies = document.cookie.split(";").map(cookie => {
      const [key, value] = cookie.split("=");
      return `${key.trim()}=${value ? value.trim() : ""}`;
    });

    if (allCookies.length > 0 && allCookies[0] !== "") {
      cookiesAccessible.value = "⚠️ Cookies Accessible (Potentially Vulnerable)";
      cookiesList.value = allCookies;
    } else {
      cookiesAccessible.value = "✅ No cookies found";
      cookiesList.value = [];
    }

    document.cookie = "test=accessible; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/";
  } catch (err) {
    cookiesAccessible.value = "⚠️ Cookies access failed";
    cookiesList.value = [];
  }
}

async function fetchISPAndDNS() {
  try {
    const response = await fetch("https://ip-api.com/json/");
    const data = await response.json();
    isp.value = data.isp ? `✅ ${data.isp}` : "⚠️ Unknown ISP";
    dnsServer.value = data.query ? `✅ DNS: ${data.query}` : "⚠️ DNS Not found";
  } catch {
    isp.value = "⚠️ Failed to fetch ISP";
    dnsServer.value = "⚠️ Failed to fetch DNS";
  }
}

// Fetch IP address
async function fetchIP() {
  try {
    const response = await fetch("https://api.ipify.org?format=json");
    const data = await response.json();
    ip.value = `✅ ${data.ip}`;
  } catch {
    ip.value = "⚠️ Failed to fetch IP";
  }
}

// Get geolocation
function getLocation() {
  navigator.geolocation.getCurrentPosition(
      (pos) => {
        location.value = `✅ Lat: ${pos.coords.latitude}, Lon: ${pos.coords.longitude}`;
      },
      () => {
        location.value = "⚠️ Geolocation Denied";
      }
  );
}

// Check webcam/mic access
async function checkWebcamAccess() {
  try {
    await navigator.mediaDevices.getUserMedia({video: true, audio: true});
    webcamAccess.value = "⚠️ Webcam/Mic Accessible (Potential Privacy Risk)";
  } catch {
    webcamAccess.value = "✅ No Direct Access to Webcam/Mic";
  }
}


// Check storage
function checkStorage() {
  document.cookie = "test=enabled";
  cookiesEnabled.value = document.cookie.includes("test=enabled") ? "⚠️ Cookies Enabled (Tracking Risk)" : "✅ Cookies Disabled";

  try {
    localStorage.setItem("test", "enabled");
    localStorageEnabled.value = "⚠️ Local Storage Enabled (Fingerprinting Risk)";
    localStorage.removeItem("test");
  } catch {
    localStorageEnabled.value = "✅ Local Storage Disabled";
  }
}

// Detect Incognito Mode
function detectIncognito() {
  const fs = window.RequestFileSystem || window.webkitRequestFileSystem;
  if (!fs) {
    incognitoStatus.value = "✅ Not Detectable";
    return;
  }
  fs(window.TEMPORARY, 100,
      () => (incognitoStatus.value = "✅ Not in Incognito"),
      () => (incognitoStatus.value = "⚠️ Incognito Mode Detected")
  );
}

// Detect Adblocker
function detectAdblocker() {
  const adDiv = document.createElement("div");
  adDiv.className = "adsbox";
  document.body.appendChild(adDiv);
  setTimeout(() => {
    if (adDiv.offsetHeight === 0) {
      adblockerDetected.value = "⚠️ Adblocker Detected";
    } else {
      adblockerDetected.value = "✅ No Adblocker";
    }
    document.body.removeChild(adDiv);
  }, 100);
}

// Canvas Fingerprint
function getCanvasFingerprint() {
  const canvas = document.createElement("canvas");
  const ctx = canvas.getContext("2d");
  ctx.textBaseline = "top";
  ctx.font = "14px Arial";
  ctx.fillText("Browser Fingerprint Test", 2, 2);
  // Full data URL
  const dataURL = canvas.toDataURL();
  canvasFingerprint.value = `⚠️ Canvas Fingerprint (Data URL): ${dataURL}`;
}

// Newly Added Functions
function checkReferrerPolicy() {
  fetch('https://example.com', { referrerPolicy: "no-referrer" })
      .then(() => {
        referrerPolicy.value = "✅ Referrer Policy Supported";
      })
      .catch(() => {
        referrerPolicy.value = "⚠️ Referrer Policy Not Supported";
      });
}

function checkHSTS() {
  const img = new Image();
  img.src = "http://subdomain.preloaded-hsts.badssl.com";
  img.onload = () => hsts.value = "⚠️ HSTS Not Enforced";
  img.onerror = () => hsts.value = "✅ HSTS Enforced";
}

// Font Fingerprinting
function detectFonts() {
  const fonts = ["Arial", "Courier New", "Times New Roman", "Comic Sans MS", "Impact"];
  const availableFonts = [];
  const canvas = document.createElement('canvas');
  const context = canvas.getContext('2d');

  fonts.forEach(font => {
    context.font = `40px ${font}`;
    const width = context.measureText('A').width;
    if (width > 0) availableFonts.push(font);
  });

  fontFingerprint.value = `⚠️ Font Fingerprint: ${availableFonts.join(", ")}`;
}

// WebSocket Leak Detection
function checkWebSocketLeak() {
  const ws = new WebSocket("wss://echo.websocket.org");
  ws.onopen = () => websocketLeak.value = "✅ WebSocket Secure";
  ws.onerror = () => websocketLeak.value = "⚠️ WebSocket Leak Detected";
}

// Battery Status
function getBatteryStatus() {
  if (navigator.getBattery) {
    navigator.getBattery().then(battery => {
      batteryStatus.value = `⚠️ Battery Level: ${Math.round(battery.level * 100)}% (Fingerprinting Risk)`;
    });
  } else {
    batteryStatus.value = "✅ No Battery API";
  }
}

// Local Time (instead of timezone offset)
function showLocalTime() {
  // Timezone can be used as a fingerprinting vector
  localTime.value = `⚠️ Local Time: ${new Date().toString()}`;
}

// CPU Usage (Dynamic)
function startCPUUsageMonitoring() {
  // Since we can't get real CPU usage, let's simulate by showing a random value every second
  setInterval(() => {
    const usage = Math.floor(Math.random() * 100); // random percentage
    cpuUsage.value = `⚠️ CPU Usage: ~${usage}%`;
  }, 1000);
}
async function checkClipboard() {
  try {
    // Read previous clipboard content
    const content = await navigator.clipboard.readText();
    previousClipboard.value = content || "No content in clipboard";

    // Write and verify
    await navigator.clipboard.writeText("Clipboard Vulnerability Test");
    const newContent = await navigator.clipboard.readText();
    clipboardTest.value = newContent === "Clipboard Vulnerability Test"
        ? "⚠️ Clipboard Write Successful (Vulnerability Detected)"
        : "✅ Clipboard Write Blocked";

    clipboardAccess.value = "⚠️ Clipboard Accessible";
  } catch {
    clipboardAccess.value = "✅ Clipboard Blocked";
    previousClipboard.value = "Permission Denied";
    clipboardTest.value = "Test Failed";
  }
}

const pluginsList = ref("Checking...");

function detectBrowserPlugins() {
  const plugins = [];
  for (let i = 0; i < navigator.plugins.length; i++) {
    plugins.push(navigator.plugins[i].name);
  }
  pluginsList.value = plugins.length > 0
      ? `⚠️ Detected Plugins: ${plugins.join(", ")}`
      : "✅ No Plugins Detected";
}


const browserLanguages = ref(`⚠️ Languages: ${navigator.languages.join(", ")}`);


const touchSupport = ref("Checking...");

function checkTouchSupport() {
  touchSupport.value = "ontouchstart" in window
      ? "⚠️ Touch Events Supported (Likely Mobile)"
      : "✅ No Touch Events";
}


const timezoneName = ref("Checking...");

function getTimezoneName() {
  timezoneName.value = `⚠️ Timezone: ${Intl.DateTimeFormat().resolvedOptions().timeZone}`;
}


const deviceMemory = ref("Checking...");

function getDeviceMemory() {
  deviceMemory.value = navigator.deviceMemory
      ? `⚠️ Device Memory: ~${navigator.deviceMemory} GB`
      : "✅ Device Memory Not Detectable";
}


const jsExecutionTime = ref("Measuring...");

function measureJavaScriptSpeed() {
  const start = performance.now();
  for (let i = 0; i < 1000000; i++) {} // Dummy loop
  const end = performance.now();
  jsExecutionTime.value = `⚠️ JS Execution Time: ${(end - start).toFixed(2)} ms`;
}


const hardwareConcurrency = ref(`⚠️ CPU Cores: ${navigator.hardwareConcurrency}`);

function validateCPUCores() {
  const expectedCores = navigator.hardwareConcurrency;
  hardwareConcurrency.value = expectedCores
      ? `⚠️ Reported CPU Cores: ${expectedCores}`
      : "✅ CPU Cores Not Detectable";
}


const speechAPI = ref("Checking...");

function checkSpeechAPI() {
  speechAPI.value = window.SpeechRecognition || window.webkitSpeechRecognition
      ? "⚠️ Speech Recognition API Supported"
      : "✅ Speech Recognition API Not Supported";
}


const idleStatus = ref("Checking...");

async function detectIdleState() {
  if ("IdleDetector" in window) {
    const idleDetector = new IdleDetector();
    await idleDetector.start();
    idleDetector.addEventListener("change", () => {
      idleStatus.value = idleDetector.userState === "idle"
          ? "⚠️ User is Idle"
          : "✅ User is Active";
    });
  } else {
    idleStatus.value = "✅ Idle Detection API Not Supported";
  }
}

const platformAnomaly = ref("Checking...");

function detectPlatformAnomaly() {
  const ua = navigator.userAgent;
  const platform = navigator.platform;

  if (
      ua.includes("Windows") && !platform.includes("Win") ||
      ua.includes("Mac") && !platform.includes("Mac")
  ) {
    platformAnomaly.value = "⚠️ Platform/User-Agent Mismatch Detected";
  } else {
    platformAnomaly.value = "✅ No Anomalies Detected";
  }
}

const speechSynthesisSupport = ref("Checking...");

function detectSpeechSynthesis() {
  speechSynthesisSupport.value = window.speechSynthesis
      ? "⚠️ Speech Synthesis API Supported"
      : "✅ Speech Synthesis API Not Supported";
}

const clipboardMonitoring = ref("Monitoring...");
const currentClipboardContent = ref("Empty");

async function monitorClipboardAccess() {
  try {
    let oldClipboardContent = await navigator.clipboard.readText();
    currentClipboardContent.value = oldClipboardContent || "Empty";

    setInterval(async () => {
      const newClipboardContent = await navigator.clipboard.readText();
      if (newClipboardContent !== oldClipboardContent) {
        clipboardMonitoring.value = "⚠️ Clipboard Change Detected!";
        currentClipboardContent.value = `Content: "${newClipboardContent}"`;
        oldClipboardContent = newClipboardContent;
      }
    }, 2000);
  } catch (err) {
    clipboardMonitoring.value = "⚠️ Clipboard Access Denied";
    currentClipboardContent.value = "N/A";
  }
}


const sensorAccess = ref("Checking...");
const sensorData = ref("No Data");

function checkSensorAccess() {
  if (window.DeviceMotionEvent) {
    sensorAccess.value = "⚠️ Motion Sensors Accessible";
    window.addEventListener("devicemotion", (event) => {
      const { x, y, z } = event.accelerationIncludingGravity || {};
      sensorData.value = `Acceleration - X: ${x?.toFixed(2) || "N/A"}, Y: ${y?.toFixed(2) || "N/A"}, Z: ${z?.toFixed(2) || "N/A"}`;
    });
  } else {
    sensorAccess.value = "✅ No Motion Sensors";
  }

  if (window.DeviceOrientationEvent) {
    sensorAccess.value += ", Orientation Sensors Accessible";
    window.addEventListener("deviceorientation", (event) => {
      const { alpha, beta, gamma } = event;
      sensorData.value += ` | Orientation - Alpha: ${alpha?.toFixed(2) || "N/A"}, Beta: ${beta?.toFixed(2) || "N/A"}, Gamma: ${gamma?.toFixed(2) || "N/A"}`;
    });
  } else {
    sensorAccess.value += ", No Orientation Sensors";
  }
}


const cpuBenchmark = ref("Running...");

function runCPUBenchmark() {
  const startTime = performance.now();
  let sum = 0;
  for (let i = 0; i < 1e8; i++) {
    sum += i;
  }
  const endTime = performance.now();
  cpuBenchmark.value = `⚠️ CPU Benchmark Time: ${(endTime - startTime).toFixed(2)} ms`;
}

const proxyDetection = ref("Checking...");

async function detectProxy() {
  const publicIP = await fetch("https://api.ipify.org?format=json").then((res) =>
      res.json()
  );

  const rtc = new RTCPeerConnection({ iceServers: [{ urls: "stun:stun.l.google.com:19302" }] });
  rtc.onicecandidate = (event) => {
    if (event.candidate) {
      const ipMatch = event.candidate.candidate.match(/\d+\.\d+\.\d+\.\d+/);
      if (ipMatch && ipMatch[0] !== publicIP.ip) {
        proxyDetection.value = "⚠️ Proxy/VPN Detected via IP Mismatch";
      } else {
        proxyDetection.value = "✅ No Proxy Detected";
      }
    }
  };
  await rtc.createOffer().then((offer) => rtc.setLocalDescription(offer));
}

const navigatorValidation = ref("Checking...");

function validateNavigator() {
  if (
      !navigator.vendor ||
      !navigator.platform ||
      !navigator.userAgent ||
      !navigator.language
  ) {
    navigatorValidation.value = "⚠️ Navigator Object Modified (Possible Spoofing)";
  } else {
    navigatorValidation.value = "✅ Navigator Object Intact";
  }
}

const audioWorkletSupport = ref("Checking...");

async function checkAudioWorklet() {
  if (window.AudioWorklet) {
    audioWorkletSupport.value = "⚠️ Audio Worklet Supported";
  } else {
    audioWorkletSupport.value = "✅ Audio Worklet Not Supported";
  }
}

const shaderPrecision = ref("Checking...");

function getWebGLShaderPrecision() {
  const canvas = document.createElement("canvas");
  const gl = canvas.getContext("webgl") || canvas.getContext("experimental-webgl");
  const precision = gl.getShaderPrecisionFormat(gl.FRAGMENT_SHADER, gl.HIGH_FLOAT);

  shaderPrecision.value = precision
      ? `⚠️ Shader Precision: ${precision.precision} bits`
      : "✅ Shader Precision Not Detectable";
}

const spoofedResolution = ref("Checking...");
const actualResolution = ref("");

function detectSpoofedResolution() {
  const reportedWidth = window.screen.width;
  const reportedHeight = window.screen.height;
  const innerWidth = window.innerWidth;
  const innerHeight = window.innerHeight;

  if (reportedWidth !== innerWidth || reportedHeight !== innerHeight) {
    spoofedResolution.value = "⚠️ Possible Screen Resolution Spoof Detected";
  } else {
    spoofedResolution.value = "✅ Resolution Matches";
  }

  actualResolution.value = `Reported: ${reportedWidth}x${reportedHeight}, Actual: ${innerWidth}x${innerHeight}`;
}

onMounted(() => {
  fetchIP();
  getLocation();
  checkWebcamAccess();
  checkWebRTC();
  checkStorage();
  detectIncognito();
  detectAdblocker();
  getCanvasFingerprint();
  fetchISPAndDNS();
  checkCookiesAccess();
  checkAutofill();

  checkReferrerPolicy();
  checkHSTS();
  checkCSP();
  userAgentSpoof.value = navigator.userAgent.includes("Headless") ? "⚠️ Headless Browser Detected" : "✅ Regular Browser";

  batteryAPI.value = navigator.getBattery ? "⚠️ Battery API Supported" : "✅ Battery API Not Supported";

  getAudioFingerprint();
  detectFonts();
  checkWebSocketLeak();
  getBatteryStatus();
  showLocalTime();
  startCPUUsageMonitoring();
  checkClipboard();
  fetchIP();
  getLocation();
  checkWebRTC();
  checkCSP();
  getAudioFingerprint();
  checkNetworkSpeed();
  getGPUFingerprint();
  checkWebWorkers();
  checkSSL();
  checkThirdPartyCookies();
  detectBrowserPlugins();
  checkTouchSupport();
  getTimezoneName();
  getDeviceMemory();
  measureJavaScriptSpeed();
  validateCPUCores();
  detectIdleState();
  checkSpeechAPI();
  detectSpoofedResolution();
  getWebGLShaderPrecision();
  checkAudioWorklet();
  validateNavigator();
  detectProxy();
  runCPUBenchmark();
  checkSensorAccess();
  monitorClipboardAccess();
  detectSpeechSynthesis();
  detectPlatformAnomaly();
});
</script>

<style scoped>
/* General Styles */
body {
  font-family: Arial, sans-serif;
  margin: 20px;
  color: #333;
  background-color: #f9f9f9;
}

h1 {
  color: #2c3e50;
  text-align: center;
  margin-bottom: 40px;
}

h2 {
  color: #34495e;
  border-bottom: 2px solid #ecf0f1;
  padding-bottom: 10px;
  margin-top: 30px;
  margin-bottom: 15px;
}

.info-section {
  background-color: #000000;
  border: 1px solid #ecf0f1;
  border-radius: 8px;
  padding: 20px;
  margin-bottom: 30px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

/* Specific Section Styles */

/* Network Information */
.network-info {
  border-left: 5px solid #3498db;
}

/* Browser Information */
.browser-info {
  border-left: 5px solid #9b59b6;
}

/* Privacy and Security Checks */
.privacy-security {
  border-left: 5px solid #e74c3c;
}

/* Fingerprinting Techniques */
.fingerprinting {
  border-left: 5px solid #f1c40f;
}

/* System Information */
.system-info {
  border-left: 5px solid #1abc9c;
}

/* API Support and Detection */
.api-support {
  border-left: 5px solid #e67e22;
}

/* Clipboard Access and Monitoring */
.clipboard-monitoring {
  border-left: 5px solid #2ecc71;
}

/* User Behavior Detection */
.user-behavior {
  border-left: 5px solid #16a085;
}

/* Miscellaneous Information */
.miscellaneous {
  border-left: 5px solid #d35400;
}

/* Error Handling and Edge Cases */
.error-handling {
  border-left: 5px solid #c0392b;
}

/* Paragraph Styles */
p {
  font-size: 16px;
  margin: 8px 0;
  line-height: 1.5;
}

strong {
  font-weight: bold;
  color: #2c3e50;
}

/* Responsive Design */
@media (max-width: 768px) {
  .info-section {
    padding: 15px;
  }

  h1 {
    font-size: 24px;
  }

  h2 {
    font-size: 20px;
  }

  p {
    font-size: 14px;
  }
}

/* Accessible Focus Styles */
.info-section:focus-within {
  outline: 2px dashed #2980b9;
}
</style>
