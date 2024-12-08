<template>
  <div id="app">
    <section>
      <p>68 74 74 70 73 3a 2f 2f 67 69 74 68 75 62 2e 63 6f 6d 2f 65 6d 72 65 75 74 6b 61 6e 2f 42 72 6f 77 73 65 72 46 69 6e 67 65 72 70 72 69 6e 74 69 6e 67 54 6f 6f 6c</p>

      <button id="theme-toggle" @click="toggleTheme">Switch Theme</button>

    </section>

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
      <p><strong>GPU Fingerprint:</strong> {{ gpuFingerprint }}</p>
      <p><strong>Font Fingerprint:</strong> {{ fontFingerprint }}</p>
      <p><strong>Shader Precision:</strong> {{ shaderPrecision }}</p>
      <p><strong>Audio Fingerprint:</strong> {{ audioFingerprint }}</p>
      <p><strong>Canvas Fingerprint:</strong> {{ canvasFingerprint }}</p>
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
      <p><strong>referrer URL: </strong>{{referrerURL}}</p>
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

    <section class="DownloadInformation">
      <h2>Download Information</h2>
      <button @click="downloadState">Download Latest State</button>
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
function downloadState() {
  // Create a content string with all the variable states
  const data = `
  IP Address: ${ip.value}
  ISP: ${isp.value}
  DNS Server: ${dnsServer.value}
  Network Speed: ${networkSpeed.value}
  SSL/TLS Version: ${sslStatus.value}
  Proxy Detection: ${proxyDetection.value}

  Browser Information:
  Browser Info: ${browser}
  User Agent Spoofing: ${userAgentSpoof.value}
  Browser Plugins: ${pluginsList.value}
  Browser Languages: ${browserLanguages.value}
  Web Workers Support: ${webWorkerSupport.value}

  Privacy and Security Checks:
  Cookies Enabled: ${cookiesEnabled.value}
  Local Storage Enabled: ${localStorageEnabled.value}
  Adblocker Detection: ${adblockerDetected.value}
  CSP Status: ${cspStatus.value}
  HSTS: ${hsts.value}
  Referrer Policy: ${referrerPolicy.value}
  Do Not Track: ${doNotTrack.value}

  Fingerprinting Techniques:
  GPU Fingerprint: ${gpuFingerprint.value}
  Font Fingerprint: ${fontFingerprint.value}
  Shader Precision: ${shaderPrecision.value}
  Audio Fingerprint: ${audioFingerprint.value}
  Canvas Fingerprint: ${canvasFingerprint.value}

  System Information:
  CPU Usage: ${cpuUsage.value}
  CPU Cores: ${cpuCores.value}
  Device Memory: ${deviceMemory.value}
  Battery Status: ${batteryStatus.value}
  Sensor Access: ${sensorAccess.value}

  API Support and Detection:
  WebRTC Public IP Leak: ${webrtcPublicIP.value}
  WebRTC Local IP Leak: ${webrtcLocalIP.value}
  WebSocket Leak: ${websocketLeak.value}
  Battery API: ${batteryAPI.value}
  Speech Recognition API: ${speechAPI.value}
  Audio Worklet Support: ${audioWorkletSupport.value}

  Clipboard Monitoring:
  Clipboard Access: ${clipboardAccess.value}
  Previous Clipboard Content: ${previousClipboard.value}
  Clipboard Test Result: ${clipboardTest.value}

  Miscellaneous Information:
  Resolution: ${resolution}
  Local Time: ${localTime.value}
  Timezone: ${timezoneName.value}
  Screen Orientation: ${screenOrientation.value}
  Pixel Ratio: ${pixelRatio.value}
  JavaScript Execution Time: ${jsExecutionTime.value}
  `;

  // Create a Blob and trigger a download
  const blob = new Blob([data], { type: "text/plain" });
  const link = document.createElement("a");
  link.href = URL.createObjectURL(blob);
  link.download = "system_info.txt";
  document.body.appendChild(link);
  link.click();
  document.body.removeChild(link);
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

const isGreenBlack = ref(false);

function toggleTheme() {
  isGreenBlack.value = !isGreenBlack.value;

  if (isGreenBlack.value) {
    document.body.classList.add("green-black");
    document.getElementById("theme-toggle").textContent = "Switch Theme";
  } else {
    document.body.classList.remove("green-black");
    document.getElementById("theme-toggle").textContent = "Switch Theme";
  }
}

onMounted(() => {
  document.body.classList.remove("green-black");
});
</script>

<style>
/* General Reset for Full-Screen View */
html, body {
  margin: 0;
  padding: 0;
  height: 100%; /* Full viewport coverage */
  width: 100%; /* Full width of the viewport */
  background-color: #121212; /* Dark gray for reduced eye strain */
  color: #dcdcdc; /* Light gray for better readability */
  font-family: "Consolas", "Lucida Console", monospace;
  overflow: hidden; /* Prevent body scroll */
  box-sizing: border-box;
}
/* Header Styling */
h1 {
  margin: 0;
  padding: 15px 0;
  font-size: 2em;
  text-align: center;
  color: #00bcd4; /* Teal for a modern accent */
  background-color: #1e1e1e; /* Slightly lighter gray for contrast */
  border-bottom: 1px solid #00bcd4;
}

/* Main Grid Container */
#app {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr)); /* Responsive grid */
  grid-auto-rows: minmax(200px, auto); /* Flexible row heights */
  gap: 10px;
  padding: 10px;
  box-sizing: border-box;
  height: calc(100vh - 65px); /* Adjusted to account for header height */
  overflow-y: auto; /* Allow vertical scroll if content overflows */
}

/* Section Container */
.info-section {
  background-color: #1e1e1e; /* Darker section background for clear distinction */
  border: 1px solid #00bcd4; /* Teal borders for clean, modern feel */
  padding: 8px;
  font-size: 13px; /* Readable text size */
  overflow: auto; /* Internal scroll for long content */
  scrollbar-width: thin;
  scrollbar-color: #00bcd4 #121212; /* Teal thumb, dark track */
}

/* WebKit Scrollbar Styling (Chrome, Safari, Edge) */
.info-section::-webkit-scrollbar {
  width: 8px;
}

.info-section::-webkit-scrollbar-track {
  background: #121212; /* Dark scrollbar track */
}

.info-section::-webkit-scrollbar-thumb {
  background: #00bcd4; /* Teal scrollbar thumb */
}

/* Section Titles */
.info-section h2 {
  font-size: 14px;
  margin: 0 0 8px 0; /* Space below title */
  padding-bottom: 5px;
  color: #00bcd4; /* Teal headings for emphasis */
  border-bottom: 1px solid #00bcd4;
}

/* Paragraph Styling */
p {
  margin: 4px 0; /* Compact spacing for readability */
  line-height: 1.3; /* Increased line height for better spacing */
  word-wrap: break-word; /* Prevents text overflow */
  color: #dcdcdc; /* Light gray text for better readability */
}

/* Bold Highlights */
strong {
  color: #ffffff; /* White for strong emphasis */
}

/* Responsive Behavior */
@media (max-width: 600px) {
  #app {
    grid-template-columns: 1fr; /* Single column layout for smaller screens */
  }

  h1 {
    font-size: 1.5em; /* Smaller title on small screens */
  }

  .info-section {
    font-size: 12px; /* Adjust text size for small screens */
  }
}


#theme-toggle {
  padding: 8px 16px;
  font-size: 14px;
  font-family: "Consolas", "Lucida Console", monospace;
  color: #ffffff;
  background-color: #000000;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s, color 0.3s;
}

#theme-toggle:hover {
  background-color: #333333;
}

body.green-black h1 {
  color: #00ff00;
  background-color: #001a00;
  border-bottom: 1px solid #00ff00;
}

body.green-black .info-section {
  background-color: #001a00;
  border: 1px solid #00ff00;
  color: #00ff00; /* Ensure all text inside inherits green */
}

body.green-black .info-section h2 {
  color: #00ff00;
  border-bottom: 1px solid #00ff00;
}

body.green-black .info-section p,
body.green-black .info-section strong,
body.green-black .info-section a,
body.green-black .info-section span {
  color: #00ff00; /* Explicitly apply green to all child elements */
}

body.green-black .info-section::-webkit-scrollbar-thumb {
  background: #00ff00; /* Green scrollbar thumb */
}

body.green-black .info-section::-webkit-scrollbar-track {
  background: #000000; /* Match background color */
}

body.green-black a {
  color: #00ff00;
  text-decoration: underline; /* Ensure links look consistent */
}
</style>
