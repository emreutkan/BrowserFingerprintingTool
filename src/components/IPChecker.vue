<template>
  <div id="app">
    <h1>Browser Vulnerability Checker</h1>
    <div>
      <p><strong>IP Address:</strong> {{ ip }}</p>
      <p><strong>ISP:</strong> {{ isp }}</p>
      <p><strong>DNS:</strong> {{ dnsServer }}</p>
      <p><strong>Resolution:</strong> {{ resolution }}</p>
      <p><strong>Geolocation:</strong> {{ location }}</p>
      <p><strong>Webcam/Mic Access:</strong> {{ webcamAccess }}</p>
      <p><strong>Browser Info:</strong> {{ browser }}</p>
      <p><strong>WebRTC Public IP Leak:</strong> {{ webrtcPublicIP }}</p>
      <p><strong>WebRTC Local IP Leak:</strong> {{ webrtcLocalIP }}</p>
      <p><strong>Cookies Enabled:</strong> {{ cookiesEnabled }}</p>
      <p><strong>Local Storage Enabled:</strong> {{ localStorageEnabled }}</p>
      <p><strong>Incognito Mode:</strong> {{ incognitoStatus }}</p>
      <p><strong>Adblocker Detection:</strong> {{ adblockerDetected }}</p>
      <p><strong>Canvas Fingerprint:</strong> {{ canvasFingerprint }}</p>
      <p><strong>Cookies Accessible:</strong> {{ cookiesAccessible }}</p>
      <p><strong>Autofill Behavior:</strong> {{ autofillDetected }}</p>

      <!-- Paranoid-Level Checks -->
      <p><strong>Referrer Policy:</strong> {{ referrerPolicy }}</p>
      <p><strong>HSTS:</strong> {{ hsts }}</p>
      <p><strong>Do Not Track (DNT):</strong> {{ doNotTrack }}</p>
      <p><strong>Battery API:</strong> {{ batteryAPI }}</p>
      <p><strong>CSP Status:</strong> {{ cspStatus }}</p>
      <p><strong>User Agent Spoofing:</strong> {{ userAgentSpoof }}</p>
      <p><strong>Audio Fingerprint:</strong> {{ audioFingerprint }}</p>
      <p><strong>Local Time:</strong> {{ localTime }}</p>
      <p><strong>Font Fingerprint:</strong> {{ fontFingerprint }}</p>
      <p><strong>WebSocket Leak:</strong> {{ websocketLeak }}</p>
      <p><strong>Battery Status:</strong> {{ batteryStatus }}</p>
      <p><strong>CPU Cores:</strong> {{ cpuCores }}</p>
      <p><strong>Network Speed:</strong> {{ networkSpeed }}</p>
      <p><strong>Screen Orientation:</strong> {{ screenOrientation }}</p>
      <p><strong>Pixel Ratio:</strong> {{ pixelRatio }}</p>
      <p><strong>SSL/TLS Version:</strong> {{ sslStatus }}</p>
      <p><strong>GPU Fingerprint:</strong> {{ gpuFingerprint }}</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

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
const autofillDetected = ref("Checking...");

// Paranoid Variables
const referrerPolicy = ref("Checking...");
const hsts = ref("Checking...");
const doNotTrack = ref(navigator.doNotTrack === "1" ? "✅ DNT Enabled" : "⚠️ DNT Disabled");
const batteryAPI = ref(navigator.getBattery ? "⚠️ Battery API Supported" : "✅ Battery API Not Supported");
const cspStatus = ref("Checking...");
const userAgentSpoof = ref(navigator.userAgent.includes("Headless") ? "⚠️ Headless Browser Detected" : "✅ Regular Browser");
const audioFingerprint = ref("Checking...");
const localTime = ref(new Date().toString());
const fontFingerprint = ref("Checking...");
const websocketLeak = ref("Checking...");
const batteryStatus = ref("Checking...");
const cpuCores = ref(`⚠️ CPU Cores: ${navigator.hardwareConcurrency}`);
const networkSpeed = ref("Checking...");
const screenOrientation = ref(`Orientation: ${screen.orientation.type}`);
const pixelRatio = ref(`Pixel Ratio: ${window.devicePixelRatio}`);
const sslStatus = ref("Checking...");
const gpuFingerprint = ref("Checking...");

// Functions
async function fetchIP() {
  try {
    const response = await fetch("https://api.ipify.org?format=json");
    const data = await response.json();
    ip.value = `✅ ${data.ip}`;
  } catch {
    ip.value = "⚠️ Failed to fetch IP";
  }
}

function getLocation() {
  navigator.geolocation.getCurrentPosition(
      (pos) => (location.value = `✅ Lat: ${pos.coords.latitude}, Lon: ${pos.coords.longitude}`),
      () => (location.value = "⚠️ Geolocation Denied")
  );
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

function getGPUFingerprint() {
  const gl = document.createElement("canvas").getContext("webgl");
  const info = gl.getExtension("WEBGL_debug_renderer_info");
  gpuFingerprint.value = info
      ? `⚠️ GPU Renderer: ${gl.getParameter(info.UNMASKED_RENDERER_WEBGL)}`
      : "✅ GPU Info Not Available";
}

function checkHSTS() {
  const img = new Image();
  img.src = "http://subdomain.preloaded-hsts.badssl.com";
  img.onload = () => (hsts.value = "⚠️ HSTS Not Enforced");
  img.onerror = () => (hsts.value = "✅ HSTS Enforced");
}

onMounted(() => {
  fetchIP();
  getLocation();
  checkReferrerPolicy();
  checkNetworkSpeed();
  getAudioFingerprint();
  getGPUFingerprint();
  checkCSP();
  checkHSTS();
});
</script>

<style>
body {
  font-family: Arial, sans-serif;
  margin: 20px;
  color: #333;
  background-color: #f9f9f9;
}
h1 {
  color: #2c3e50;
}
p {
  font-size: 16px;
  margin: 5px 0;
}
strong {
  font-weight: bold;
}
</style>
