# kingdomchat
Connect with random people worldwide. Be respectful and kind
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Kingdom</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        .video-container {
            position: relative;
        }
        .remote-video {
            background-color: #000;
        }
        .local-video {
            position: absolute;
            bottom: 20px;
            right: 20px;
            width: 25%;
            max-width: 200px;
            background-color: #000;
            border-radius: 8px;
            box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
        }
        .emoji-panel {
            position: absolute;
            bottom: 100px;
            left: 50%;
            transform: translateX(-50%);
            display: none;
        }
        .emoji-popup {
            position: absolute;
            bottom: 150px;
            left: 50%;
            transform: translateX(-50%);
            display: none;
            animation: popup 1.5s;
        }
        @keyframes popup {
            0% { transform: translate(-50%, 0); opacity: 0; }
            20% { transform: translate(-50%, -30px); opacity: 1; }
            80% { transform: translate(-50%, -30px); opacity: 1; }
            100% { transform: translate(-50%, -60px); opacity: 0; }
        }
    </style>
</head>
<body class="bg-gray-900 text-white h-screen flex flex-col">
    <header class="bg-gray-800 p-4 shadow-md">
        <div class="container mx-auto flex justify-between items-center">
            <h1 class="text-2xl font-bold">Kingdom</h1>
            <div id="connection-status" class="flex items-center">
                <div class="w-3 h-3 rounded-full bg-red-500 mr-2"></div>
                <span>Disconnected</span>
            </div>
        </div>
    </header>

    <main class="flex-1 flex flex-col items-center justify-center p-4">
        <div class="video-container w-full max-w-4xl h-96 mb-8 rounded-lg overflow
            <video id="remote-video" class="remote-video w-full h-full object-cove
            <video id="local-video" class="local-video" autoplay playsinline muted
            
            <div id="emoji-popup" class="emoji-popup text-5xl">👋</div>
            <div id="emoji-panel" class="emoji-panel bg-gray-800 p-2 rounded-lg fl
                <button class="emoji-btn text-3xl hover:scale-110 transition-trans
                <button class="emoji-btn text-3xl hover:scale-110 transition-trans
                <button class="emoji-btn text-3xl hover:scale-110 transition-trans
                <button class="emoji-btn text-3xl hover:scale-110 transition-trans
                <button class="emoji-btn text-3xl hover:scale-110 transition-trans
            </div>
        </div>

        <div class="flex flex-col items-center mb-8" id="pre-connection">
            <div class="mb-6">
                <h2 class="text-xl mb-2">Select preferred gender:</h2>
                <div class="flex gap-4">
                    <label class="flex items-center">
                        <input type="radio" name="gender" value="male" class="mr-2
                        Male
                    </label>
                    <label class="flex items-center">
                        <input type="radio" name="gender" value="female" class="mr
                        Female
                    </label>
                    <label class="flex items-center">
                        <input type="radio" name="gender" value="both" class="mr-2
                        Both
                    </label>
                </div>
            </div>

            <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-

            <button id="start-btn" class="bg-blue-600 hover:bg-blue-700 text-white
                Start Chatting
            </button>
        </div>

        <div id="controls" class="hidden bg-gray-800 p-4 rounded-lg flex gap-4">
            <button id="emoji-btn" class="bg-yellow-600 hover:bg-yellow-700 text-w
                Emoji Reaction
            </button>
            <button id="mic-toggle" class="bg-blue-600 hover:bg-blue-700 text-whit
                Mute
            </button>
            <button id="video-toggle" class="bg-blue-600 hover:bg-blue-700 text-wh
                Hide Webcam
            </button>
            <button id="next-btn" class="bg-green-600 hover:bg-green-700 text-whit
                Next Stranger
            </button>
            <button id="end-btn" class="bg-red-600 hover:bg-red-700 text-white p-3
                End Call
            </button>
        </div>
    </main>

    <footer class="bg-gray-800 p-4 text-center text-gray-400">
        <p>Connect with random people worldwide. Be respectful and kind© 2023 gpst
    </footer>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            // DOM Elements
            const remoteVideo = document.getElementById('remote-video');
            const localVideo = document.getElementById('local-video');
            const startBtn = document.getElementById('start-btn');
            const emojiBtn = document.getElementById('emoji-btn');
            const emojiPanel = document.getElementById('emoji-panel');
            const emojiPopup = document.getElementById('emoji-popup');
            const controls = document.getElementById('controls');
            const preConnection = document.getElementById('pre-connection');
            const connectionStatus = document.getElementById('connection-status');
            const micToggle = document.getElementById('mic-toggle');
            const videoToggle = document.getElementById('video-toggle');
            const nextBtn = document.getElementById('next-btn');
            const endBtn = document.getElementById('end-btn');
            
            // State variables
            let localStream;
            let peerConnection;
            let selectedGender = 'male';
            
            // Gender selection
            document.querySelectorAll('input[name="gender"]').forEach(radio => {
                radio.addEventListener('change', (e) => {
                    selectedGender = e.target.value;
                });
            });
            
            // Simulated connection for demo purposes
            startBtn.addEventListener('click', async () => {
                try {
                    // Get user media (in a real app, this would trigger WebRTC co
                    localStream = await navigator.mediaDevices.getUserMedia({
                        video: true,
                        audio: true
                    });
                    
                    localVideo.srcObject = localStream;
                    
                    // Hide pre-connection UI and show controls
                    preConnection.classList.add('hidden');
                    controls.classList.remove('hidden');
                    connectionStatus.querySelector('div').classList.replace('bg-re
                    connectionStatus.querySelector('span').textContent = 'Connecte
                    
                    // Show simulated remote video
                    setTimeout(() => {
                        remoteVideo.srcObject = localStream;
                        remoteVideo.classList.add('mirror');
                    }, 1500);
                    
                } catch (err) {
                    console.error('Error accessing media devices:', err);
                    alert('Could not access camera/microphone. Please ensure you h
                }
            });
            
            // Emoji panel toggle
            emojiBtn.addEventListener('click', () => {
                emojiPanel.style.display = emojiPanel.style.display === 'flex' ? '
            });
            
            // Emoji selection
            document.querySelectorAll('.emoji-btn').forEach(btn => {
                btn.addEventListener('click', () => {
                    const emoji = btn.getAttribute('data-emoji');
                    emojiPopup.textContent = emoji;
                    emojiPopup.style.display = 'block';
                    emojiPanel.style.display = 'none';
                    
                    setTimeout(() => {
                        emojiPopup.style.display = 'none';
                    }, 1500);
                });
            });
            
            // Media control toggles
            micToggle.addEventListener('click', () => {
                const muted = !localStream.getAudioTracks()[0].enabled;
                localStream.getAudioTracks()[0].enabled = muted;
                micToggle.textContent = muted ? 'Mute' : 'Unmute';
            });
            
            videoToggle.addEventListener('click', () => {
                const enabled = !localStream.getVideoTracks()[0].enabled;
                localStream.getVideoTracks()[0].enabled = enabled;
                videoToggle.textContent = enabled ? 'Hide Webcam' : 'Show Webcam';
                localVideo.style.display = enabled ? 'block' : 'none';
            });
            
            // Next stranger button
            nextBtn.addEventListener('click', () => {
                alert('Connecting to next stranger...');
                // In a real app, this would initiate new peer connection
            });
            
            // End call button
            endBtn.addEventListener('click', () => {
                if (localStream) {
                    localStream.getTracks().forEach(track => track.stop());
                }
                if (remoteVideo.srcObject) {
                    remoteVideo.srcObject.getTracks().forEach(track => track.stop(
                }
                
                remoteVideo.srcObject = null;
                localVideo.srcObject = null;
                
                controls.classList.add('hidden');
                preConnection.classList.remove('hidden');
                connectionStatus.querySelector('div').classList.replace('bg-green-
                connectionStatus.querySelector('span').textContent = 'Disconnected
                
                alert('Call ended. You can start a new call.');
            });
        });
    </script>
</body>
</html>

