<!DOCTYPE html>
<html lang="hi">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cricket Central</title>
    <style>
        :root {
            --primary: #009688;
            --primary-dark: #00796b;
            --bg-light: #f4f6f9;
            --card-bg: #ffffff;
            --text-main: #333333;
            --text-muted: #666666;
            --accent: #ff9800;
            --danger: #dc3545;
        }
        body { 
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; 
            background: var(--bg-light); 
            margin: 0; 
            padding: 0; 
            color: var(--text-main); 
        }
        .app-header {
            background: var(--primary);
            color: white;
            padding: 15px 20px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        .app-header h2 { margin: 0; font-size: 20px; }
        .admin-badge-btn {
            background: white;
            color: var(--primary);
            border: none;
            padding: 6px 12px;
            border-radius: 4px;
            font-weight: bold;
            cursor: pointer;
        }
        .tabs-container {
            background: var(--primary-dark);
            display: flex;
            justify-content: space-around;
            padding: 0 10px;
        }
        .tab-btn {
            background: none;
            border: none;
            color: rgba(255,255,255,0.7);
            padding: 12px 15px;
            font-weight: bold;
            cursor: pointer;
            font-size: 14px;
            text-transform: uppercase;
        }
        .tab-btn.active {
            color: white;
            border-bottom: 3px solid white;
        }
        .container { max-width: 500px; margin: auto; padding: 15px; }
        .card { 
            background: var(--card-bg); 
            padding: 15px; 
            border-radius: 8px; 
            margin-bottom: 15px; 
            box-shadow: 0 2px 8px rgba(0,0,0,0.05);
            border: 1px solid #e0e0e0;
        }
        input, select, button { 
            width: 100%; 
            padding: 10px; 
            margin-top: 8px; 
            border: 1px solid #ccc; 
            border-radius: 6px; 
            box-sizing: border-box; 
            font-size: 14px;
        }
        button.action-btn { 
            background: var(--primary); 
            color: white; 
            border: none; 
            font-weight: bold; 
            cursor: pointer; 
        }
        button.action-btn:hover { background: var(--primary-dark); }
        .logout-btn { background: var(--danger); color: white; margin-top: 10px; border: none; font-weight: bold; padding: 10px; border-radius: 6px; cursor: pointer;}
        .hidden { display: none !important; }
        
        .series-title {
            background: #e0f2f1;
            color: var(--primary-dark);
            padding: 8px 12px;
            font-weight: bold;
            border-radius: 6px;
            margin-bottom: 10px;
            font-size: 14px;
        }
        .series-title.with-gap { margin-top: 25px; }
        .series-title.no-gap { margin-top: 5px; }
        .match-box {
            background: #fff;
            border: 1px solid #e0e0e0;
            border-radius: 8px;
            padding: 12px;
            margin-bottom: 10px;
            box-shadow: 0 1px 3px rgba(0,0,0,0.05);
        }
        .match-info-top {
            display: flex;
            justify-content: space-between;
            font-size: 12px;
            color: var(--text-muted);
            margin-bottom: 6px;
        }
        .match-teams {
            display: flex;
            justify-content: space-between;
            align-items: center;
            font-weight: bold;
            font-size: 15px;
            margin: 8px 0;
        }
        .match-toss-banner {
            background: #e0f2f1;
            color: #00796b;
            padding: 5px 8px;
            font-size: 12px;
            border-radius: 4px;
            margin-top: 6px;
            font-weight: bold;
        }
        .match-result-banner {
            background: #ffebee;
            color: #c62828;
            padding: 5px 8px;
            font-size: 12px;
            border-radius: 4px;
            margin-top: 6px;
            font-weight: bold;
        }
        table { width: 100%; border-collapse: collapse; margin-top: 5px; font-size: 13px; }
        th, td { border: 1px solid #e0e0e0; padding: 8px; text-align: center; }
        th { background: #e0f2f1; color: var(--primary-dark); font-weight: bold; }
        tr:nth-child(even) { background-color: #fafafa; }
        .plan-box { border: 1px solid var(--primary); padding: 10px; border-radius: 6px; margin-top: 8px; background: #f9f9f9; }
        .admin-section-box { background: #fffde7; border: 1px solid #ffe082; padding: 12px; border-radius: 8px; margin-bottom: 15px; }
        .admin-section-box h4 { margin-top: 0; color: #f57c00; font-size: 15px; border-bottom: 1px dashed #ffe082; padding-bottom: 5px; }
    </style>
</head>
<body>

    <div class="app-header">
        <h2>Cricket Central</h2>
        <button class="admin-badge-btn" id="adminBtn">Admin</button>
    </div>

    <div id="appTabs" class="tabs-container hidden">
        <button class="tab-btn active" data-tab="matches">Matches</button>
        <button class="tab-btn" data-tab="points">Points Table</button>
        <button class="tab-btn" data-tab="groups">Groups</button>
        <button class="tab-btn" data-tab="wallet">Wallet</button>
    </div>

<div class="container">
    <!-- LOGIN SCREEN -->
    <div id="loginSection" class="card">
        <h3>Cricket App Login</h3>
        <p style="text-align: center; font-size: 13px; color: var(--text-muted);">Aage badhne ke liye apna phone number dalein:<br><span style="color: var(--primary); font-weight: bold;">(Naye number par 15 Free Points milenge!)</span></p>
        
        <div id="phoneStep">
            <input type="tel" id="userPhoneInput" placeholder="Apna Mobile Number Dalein" maxlength="10">
            <button class="action-btn" id="sendOtpBtn">OTP Bhejein</button>
        </div>

        <div id="otpStep" class="hidden" style="margin-top: 15px; border-top: 1px dashed #ccc; padding-top: 10px;">
            <p style="font-size: 13px; color: #2e7d32; text-align: center;">Aapke number par OTP bheja gaya hai.</p>
            <input type="number" id="otpInput" placeholder="4-digit OTP Dalein" maxlength="4">
            <button class="action-btn" id="verifyOtpBtn" style="background: #2e7d32;">Verify & Login Karein</button>
            <button id="resetLoginBtn" style="background: #757575; color:white; border:none; padding:8px; border-radius:6px; margin-top:5px; width:100%; cursor:pointer;">Number Badlein</button>
        </div>
    </div>

    <!-- MAIN DASHBOARD CONTAINER -->
    <div id="dashboardSection" class="hidden">
        
        <!-- TAB 1: MATCHES -->
        <div id="tabMatches" class="tab-content">
            <div class="card">
                <h3>📅 Live & Upcoming Schedule</h3>
                <div id="scheduleList"></div>
            </div>
        </div>

        <!-- TAB 2: POINTS TABLE -->
        <div id="tabPoints" class="tab-content hidden">
            <div id="pointsTablesDisplayContainer"></div>
        </div>

        <!-- TAB 3: GROUPS -->
        <div id="tabGroups" class="tab-content hidden">
            <div class="card">
                <h3>👥 Group Management</h3>
                <p style="font-size: 12px; color: var(--text-muted);">Aap unlimited teams ke sath kitne bhi groups bana sakte hain.</p>
                <div id="groupsContainer" style="margin-top: 10px;"></div>
            </div>
        </div>

        <!-- TAB 4: WALLET & SUBSCRIPTION -->
        <div id="tabWallet" class="tab-content hidden">
            <div class="card" style="background: #e0f2f1;">
                <h3 style="color: var(--primary-dark);">💰 Aapka Wallet</h3>
                <p style="font-size: 16px; text-align: center;"><strong>Available Points:</strong> <span id="userPoints" style="color: var(--primary); font-weight: bold; font-size: 20px;">0</span></p>
                <p id="subStatus" style="text-align: center; font-weight: bold; color: #2e7d32; font-size: 13px;"></p>
            </div>

            <!-- REDEEM CODE SECTION -->
            <div class="card" style="border: 1px dashed var(--primary);">
                <h3>🎟️ Redeem Code Dalein</h3>
                <input type="text" id="redeemCodeInput" placeholder="6-digit code dalein (jaise: Ab3X9y)" style="text-transform: uppercase;">
                <button class="action-btn" id="redeemCodeBtn">Code Redeem Karein</button>
            </div>

            <div class="card">
                <h3>⭐ Subscription Plans</h3>
                <p style="font-size: 12px; color: var(--text-muted); text-align: center;">App aur Admin features unlock karne ke liye plan lein:</p>
                
                <div class="plan-box">
                    <p style="margin: 0 0 5px 0;"><strong>3 Match Subscription:</strong> 99 Points</p>
                    <button class="action-btn buy-sub-btn" data-cost="99" data-plan="3 Match Subscription">Buy 3 Match Plan</button>
                </div>
                <div class="plan-box">
                    <p style="margin: 0 0 5px 0;"><strong>30 Minutes Plan:</strong> 149 Points</p>
                    <button class="action-btn buy-sub-btn" data-cost="149" data-plan="30 Minutes Plan">Buy 30 Mins Plan</button>
                </div>
                <div class="plan-box">
                    <p style="margin: 0 0 5px 0;"><strong>Half Monthly Plan:</strong> 400 Points</p>
                    <button class="action-btn buy-sub-btn" data-cost="400" data-plan="Half Monthly Plan">Buy Half Monthly</button>
                </div>
                <div class="plan-box">
                    <p style="margin: 0 0 5px 0;"><strong>Monthly Plan:</strong> 600 Points</p>
                    <button class="action-btn buy-sub-btn" data-cost="600" data-plan="Monthly Plan">Buy Monthly</button>
                </div>
                <div class="plan-box">
                    <p style="margin: 0 0 5px 0;"><strong>Half Yearly Plan:</strong> 6000 Points</p>
                    <button class="action-btn buy-sub-btn" data-cost="6000" data-plan="Half Yearly Plan">Buy Half Yearly</button>
                </div>
                <div class="plan-box">
                    <p style="margin: 0 0 5px 0;"><strong>Yearly Plan:</strong> 8000 Points</p>
                    <button class="action-btn buy-sub-btn" data-cost="8000" data-plan="Yearly Plan">Buy Yearly</button>
                </div>
            </div>

            <div class="card">
                <h3>💳 Points Kaise Kharidein?</h3>
                <ul style="font-size: 13px; padding-left: 18px; color: var(--text-muted);">
                    <li>₹80 = 800 Points</li>
                    <li>₹150 = 1500 Points</li>
                    <li>₹249 = 4000 Points</li>
                </ul>
                <p style="text-align: center; font-weight: bold; color: var(--danger);">Sampark Karein: 9569981484</p>
            </div>
        </div>

        <!-- ADMIN PANEL SECTION -->
        <div id="adminPanelSection" class="card hidden" style="border: 2px solid var(--accent); background: #fff;">
            <h3 style="color: #f57c00; margin-top:0;">👑 Admin Control Panel</h3>
            
            <!-- OPTION 1: MATCH SCHEDULE & RESULT UPDATE -->
            <div class="admin-section-box">
                <h4>1. Match Schedule & Result Update</h4>
                <input type="hidden" id="editMatchId" value="">
                <input type="text" id="seriesName" placeholder="Series Name (jaise: Sa20, 2027)">
                
                <label style="font-size: 12px; font-weight: bold; color: #333; display: block; margin-top: 6px;">Series ka Type Chunein:</label>
                <select id="seriesTypeOption">
                    <option value="same">1. Usi series ka match hai (Bina gap ke)</option>
                    <option value="new">2. New series ka match hai (Gap ke sath)</option>
                </select>

                <input type="text" id="matchFormat" placeholder="Format (jaise: 1st Match / T20)">
                <input type="text" id="team1" placeholder="Team 1 (jaise: DSG)">
                <input type="text" id="team2" placeholder="Team 2 (jaise: JSK)">
                <input type="text" id="venue" placeholder="Venue / Stadium">
                <input type="text" id="matchTossUpdate" placeholder="Toss Update (jaise: DSG won toss & elected to bat)">
                <button class="action-btn" id="saveMatchBtn" style="margin-top:8px;">Match Save Karein</button>

                <h5 style="margin: 12px 0 5px 0; color: #333;">Match Result & Scores Update</h5>
                <select id="matchSelectForUpdate"></select>
                <input type="text" id="matchWinner" placeholder="Match Winner (jaise: DSG won by 6 wickets)">
                <input type="text" id="team1ScoreDetails" placeholder="Team 1 Score (jaise: 180/4 in 20 ov)">
                <input type="text" id="team2ScoreDetails" placeholder="Team 2 Score (jaise: 175/6 in 20 ov)">
                <button class="action-btn" id="updateResultBtn" style="background: #0284c7; margin-top:8px;">Result Update Karein</button>
            </div>

            <!-- OPTION 2: REDEEM CODE GENERATE -->
            <div id="mainAdminCodeBox" class="admin-section-box hidden">
                <h4>2. Generate Redeem Code (Admin Only)</h4>
                <input type="text" id="adminCustomCode" placeholder="Code dalein (6 digit: e.g. Ab3X9y)" style="text-transform: uppercase;" maxlength="6">
                <input type="number" id="adminCodePoints" placeholder="Kitne points ka code hai?">
                <button class="action-btn" id="generateCodeBtn" style="background: #f57c00; margin-top:8px;">Redeem Code Banayein</button>
            </div>

            <!-- OPTION 3: GROUP CREATION (UNLIMITED TEAMS) -->
            <div class="admin-section-box">
                <h4>3. Group Creation (Unlimited Teams)</h4>
                <input type="text" id="groupNameInput" placeholder="Group Name (jaise: Sa20, 2027)">
                <input type="text" id="groupTeamsInput" placeholder="Teams comma se alag karein (jaise: DSG, JSK, MICT, PC, PR, SEC)">
                <button class="action-btn" id="createGroupBtn" style="margin-top:8px;">Group Banayein</button>
                <div id="adminGroupsList" style="margin-top: 10px;"></div>
            </div>

            <!-- OPTION 4: POINTS TABLE MATCH RESULT LINKED UPDATE -->
            <div class="admin-section-box">
                <h4>4. Points Table Match Result Update (ICC Formula)</h4>
                
                <label style="font-size: 12px; font-weight: bold; color: #333; display: block; margin-top: 5px;">1. Sabse Pehle Group Chunein:</label>
                <select id="ptGroupSelect">
                    <option value="">-- Group Chunein --</option>
                </select>

                <label style="font-size: 12px; font-weight: bold; color: #333; display: block; margin-top: 8px;">2. Team 1 Chunein:</label>
                <select id="ptTeam1Select">
                    <option value="">Pehle Group Chunein</option>
                </select>
                <input type="text" id="ptTeam1ScoreInput" placeholder="Team 1 Score (jaise: 180/4 in 20 ov)">

                <label style="font-size: 12px; font-weight: bold; color: #333; display: block; margin-top: 8px;">3. Team 2 Chunein:</label>
                <select id="ptTeam2Select">
                    <option value="">Pehle Group Chunein</option>
                </select>
                <input type="text" id="ptTeam2ScoreInput" placeholder="Team 2 Score (jaise: 175/6 in 20 ov)">
                
                <input type="text" id="ptCustomNrrInput" placeholder="Optional: Team 1 NRR adjust (e.g. +1.245 ya -0.500)" style="margin-top:8px;">

                <button class="action-btn" id="savePointTableMatchBtn" style="margin-top: 10px; background: var(--primary-dark);">Points Table Update Karein</button>
                <div id="adminPtTablesList" style="margin-top: 10px;"></div>
            </div>
            
            <button id="closeAdminBtn" class="logout-btn" style="background: #757575;">Admin Panel Band Karein</button>
        </div>

        <button class="logout-btn" id="logoutBtn">Logout</button>
    </div>
</div>

<script>
    const ADMIN_NUMBER = "9569981484";
    let generatedOTP = "";
    let tempPhone = "";
    let isAdminUnlocked = false;

    function getUsers() { return JSON.parse(localStorage.getItem('app_users')) || {}; }
    function saveUsers(users) { localStorage.setItem('app_users', JSON.stringify(users)); }
    
    function getMatches() { return JSON.parse(localStorage.getItem('app_matches')) || []; }
    function saveMatches(matches) { localStorage.setItem('app_matches', JSON.stringify(matches)); }

    function getPointsTables() { return JSON.parse(localStorage.getItem('app_points_tables_v2')) || {}; }
    function savePointsTables(tables) { localStorage.setItem('app_points_tables_v2', JSON.stringify(tables)); }

    function getGroups() { return JSON.parse(localStorage.getItem('app_groups')) || {}; }
    function saveGroups(groups) { localStorage.setItem('app_groups', JSON.stringify(groups)); }

    function getDeviceLogins() { return JSON.parse(localStorage.getItem('device_logged_numbers')) || []; }
    function saveDeviceLogins(list) { localStorage.setItem('device_logged_numbers', JSON.stringify(list)); }

    function getRedeemCodes() { return JSON.parse(localStorage.getItem('app_redeem_codes')) || {}; }
    function saveRedeemCodes(codes) { localStorage.setItem('app_redeem_codes', JSON.stringify(codes)); }

    function sendOTP() {
        let phone = document.getElementById('userPhoneInput').value.trim();
        if(phone.length !== 10) {
            alert("Kripya sahi 10-digit ka mobile number dalein!");
            return;
        }

        let activeSessions = JSON.parse(localStorage.getItem('active_sessions')) || {};
        let currentActiveDevice = activeSessions[phone];
        let myDeviceId = localStorage.getItem('my_device_id');
        if(!myDeviceId) {
            myDeviceId = 'dev_' + Math.random().toString(36).substring(2);
            localStorage.setItem('my_device_id', myDeviceId);
        }

        if(currentActiveDevice && currentActiveDevice !== myDeviceId) {
            alert("Error: Ye number pehle se hi kisi doosri device par logged in hai!");
            return;
        }

        let loggedList = getDeviceLogins();
        if(!loggedList.includes(phone) && loggedList.length >= 3) {
            alert("Error: Is device par max 3 numbers se hi login karna allowed hai.");
            return;
        }

        tempPhone = phone;
        generatedOTP = Math.floor(1000 + Math.random() * 9000).toString();
        alert("Aapka OTP hai: " + generatedOTP);

        document.getElementById('phoneStep').classList.add('hidden');
        document.getElementById('otpStep').classList.remove('hidden');
    }

    function verifyOTP() {
        let enteredOTP = document.getElementById('otpInput').value.trim();
        if(enteredOTP !== generatedOTP) {
            alert("Galat OTP! Kripya sahi OTP dalein.");
            return;
        }

        let myDeviceId = localStorage.getItem('my_device_id');
        let activeSessions = JSON.parse(localStorage.getItem('active_sessions')) || {};
        activeSessions[tempPhone] = myDeviceId;
        localStorage.setItem('active_sessions', JSON.stringify(activeSessions));

        let loggedList = getDeviceLogins();
        if(!loggedList.includes(tempPhone)) {
            loggedList.push(tempPhone);
            saveDeviceLogins(loggedList);
        }

        let users = getUsers();
        if(!users[tempPhone]) {
            let initialPoints = (tempPhone === ADMIN_NUMBER ? 50000 : 15);
            users[tempPhone] = { points: initialPoints, subscription: null, subExpiry: 0, matchesLeft: 0 };
            saveUsers(users);
        }

        localStorage.setItem('current_user', tempPhone);
        loadDashboard();
    }

    function resetLogin() {
        document.getElementById('phoneStep').classList.remove('hidden');
        document.getElementById('otpStep').classList.add('hidden');
        document.getElementById('otpInput').value = "";
    }

    function loadDashboard() {
        let currentPhone = localStorage.getItem('current_user');
        if(!currentPhone) return;

        checkSubscriptionExpiry();

        document.getElementById('loginSection').classList.add('hidden');
        document.getElementById('dashboardSection').classList.remove('hidden');
        document.getElementById('appTabs').classList.remove('hidden');

        let users = getUsers();
        let userData = users[currentPhone];

        document.getElementById('userPoints').innerText = userData.points;

        let hasActiveSub = false;
        if(userData.subscription) {
            if(userData.subscription.includes('Match')) {
                if(userData.matchesLeft > 0) hasActiveSub = true;
            } else if(userData.subExpiry > Date.now()) {
                hasActiveSub = true;
            }
        }

        if(hasActiveSub) {
            let subText = userData.subscription;
            if(userData.subscription.includes('Match')) subText += ` (${userData.matchesLeft} Match Schedule Left)`;
            document.getElementById('subStatus').innerHTML = "Active Plan: <span style='color:#009688;'>" + subText + "</span>";
        } else {
            userData.subscription = null;
            userData.subExpiry = 0;
            userData.matchesLeft = 0;
            saveUsers(users);
            document.getElementById('subStatus').innerHTML = "<span style='color:#d32f2f;'>No Active Subscription. App use karne ke liye neeche se plan lein!</span>";
        }

        renderSchedule();
        renderAllPointsTables();
        renderGroups();
        updateMatchDropdown();
        populateAdminGroupDropdown();
        renderAdminPointsTablesList();
        renderAdminGroupsList();
    }

    function switchTab(tabName) {
        document.querySelectorAll('.tab-content').forEach(el => el.classList.add('hidden'));
        document.querySelectorAll('.tab-btn').forEach(el => el.classList.remove('active'));
        document.getElementById('adminPanelSection').classList.add('hidden');

        if(tabName === 'matches') {
            document.getElementById('tabMatches').classList.remove('hidden');
        } else if(tabName === 'points') {
            document.getElementById('tabPoints').classList.remove('hidden');
        } else if(tabName === 'groups') {
            document.getElementById('tabGroups').classList.remove('hidden');
        } else if(tabName === 'wallet') {
            document.getElementById('tabWallet').classList.remove('hidden');
        }
        event.target.classList.add('active');
    }

    function checkAdminAccess() {
        let currentPhone = localStorage.getItem('current_user');
        if(!currentPhone) {
            alert("Pehle login karein!");
            return;
        }

        checkSubscriptionExpiry();
        let users = getUsers();
        let userData = users[currentPhone];

        let hasActiveSub = false;
        if(userData.subscription) {
            if(userData.subscription.includes('Match')) {
                if(userData.matchesLeft > 0) hasActiveSub = true;
            } else if(userData.subExpiry > Date.now()) {
                hasActiveSub = true;
            }
        }
        
        if(!hasActiveSub) {
            alert("Please purchase this subscription. Koi subscription active nahi hai aap ke paas.");
            switchTab('wallet');
            return;
        }

        isAdminUnlocked = true;
        document.getElementById('adminPanelSection').classList.remove('hidden');
        
        if(currentPhone === ADMIN_NUMBER) {
            document.getElementById('mainAdminCodeBox').classList.remove('hidden');
        } else {
            document.getElementById('mainAdminCodeBox').classList.add('hidden');
        }

        renderSchedule();
        populateAdminGroupDropdown();
        renderAdminPointsTablesList();
        renderAdminGroupsList();
        alert("Admin Panel Successfully Unlocked!");
    }

    function closeAdminPanel() {
        isAdminUnlocked = false;
        document.getElementById('adminPanelSection').classList.add('hidden');
        resetMatchForm();
        renderSchedule();
    }

    function generateRedeemCode() {
        let currentPhone = localStorage.getItem('current_user');
        if(currentPhone !== ADMIN_NUMBER) {
            alert("Sirf website admin hi redeem code generate kar sakta hai!");
            return;
        }

        let code = document.getElementById('adminCustomCode').value.trim().toUpperCase();
        let points = parseInt(document.getElementById('adminCodePoints').value);

        if(code.length !== 6) {
            alert("Code 6-digit ka hona chahiye!");
            return;
        }
        if(isNaN(points) || points <= 0) {
            alert("Sahi points dalein!");
            return;
        }

        let users = getUsers();
        if(users[currentPhone].points < points) {
            alert("Aapke wallet mein itne points nahi hain!");
            return;
        }

        let codes = getRedeemCodes();
        if(codes[code]) {
            alert("Ye code pehle se exist karta hai!");
            return;
        }

        users[currentPhone].points -= points;
        saveUsers(users);

        codes[code] = points;
        saveRedeemCodes(codes);

        document.getElementById('adminCustomCode').value = "";
        document.getElementById('adminCodePoints').value = "";
        loadDashboard();
        alert("Redeem Code successfully ban gaya!");
    }

    function redeemPointsCode() {
        let currentPhone = localStorage.getItem('current_user');
        let code = document.getElementById('redeemCodeInput').value.trim().toUpperCase();

        if(!code) {
            alert("Kripya code dalein!");
            return;
        }

        let codes = getRedeemCodes();
        if(!codes[code]) {
            alert("Ye code invalid hai ya pehle hi use ho chuka hai!");
            return;
        }

        let points = codes[code];
        let users = getUsers();
        users[currentPhone].points += points;
        saveUsers(users);

        delete codes[code];
        saveRedeemCodes(codes);

        document.getElementById('redeemCodeInput').value = "";
        loadDashboard();
        alert("Badhai ho! " + points + " points aapke wallet mein add kar diye gaye hain.");
    }

    function buySubscription(cost, planName) {
        let currentPhone = localStorage.getItem('current_user');
        let users = getUsers();

        if(users[currentPhone].points < cost) {
            alert("Aapke paas subscription lene ke liye pure points nahi hain!");
            return;
        }

        users[currentPhone].points -= cost;
        
        if(!users[ADMIN_NUMBER]) users[ADMIN_NUMBER] = { points: 50000, subscription: null, subExpiry: 0, matchesLeft: 0 };
        users[ADMIN_NUMBER].points += cost;

        users[currentPhone].subscription = planName;
        if(planName === '3 Match Subscription') {
            users[currentPhone].matchesLeft = 3;
            users[currentPhone].subExpiry = 0;
        } else {
            users[currentPhone].matchesLeft = 0;
            if(planName === '30 Minutes Plan') {
                users[currentPhone].subExpiry = Date.now() + (30 * 60 * 1000);
            } else if(planName === 'Half Monthly Plan') {
                users[currentPhone].subExpiry = Date.now() + (15 * 24 * 60 * 60 * 1000);
            } else {
                users[currentPhone].subExpiry = Date.now() + (30 * 24 * 60 * 60 * 1000);
            }
        }

        saveUsers(users);
        loadDashboard();
        alert(planName + " successfully activated!");
    }

    function checkSubscriptionExpiry() {
        let currentPhone = localStorage.getItem('current_user');
        let users = getUsers();
        if(users[currentPhone] && users[currentPhone].subscription) {
            if(!users[currentPhone].subscription.includes('Match') && users[currentPhone].subExpiry < Date.now()) {
                users[currentPhone].subscription = null;
                users[currentPhone].subExpiry = 0;
                saveUsers(users);
            } else if(users[currentPhone].subscription.includes('Match') && users[currentPhone].matchesLeft <= 0) {
                users[currentPhone].subscription = null;
                users[currentPhone].matchesLeft = 0;
                saveUsers(users);
            }
        }
    }

    function populateAdminGroupDropdown() {
        let groups = getGroups();
        let groupSelect = document.getElementById('ptGroupSelect');
        let keys = Object.keys(groups);

        groupSelect.innerHTML = "<option value=''>-- Group Chunein --</option>";
        keys.forEach(gName => {
            groupSelect.innerHTML += `<option value="${gName}">${gName}</option>`;
        });
        
        document.getElementById('ptTeam1Select').innerHTML = "<option value=''>Pehle Group Chunein</option>";
        document.getElementById('ptTeam2Select').innerHTML = "<option value=''>Pehle Group Chunein</option>";
    }

    function onAdminGroupSelected() {
        let groupName = document.getElementById('ptGroupSelect').value;
        let groups = getGroups();
        let team1Select = document.getElementById('ptTeam1Select');
        let team2Select = document.getElementById('ptTeam2Select');

        if(!groupName || !groups[groupName]) {
            team1Select.innerHTML = "<option value=''>Pehle Group Chunein</option>";
            team2Select.innerHTML = "<option value=''>Pehle Group Chunein</option>";
            return;
        }

        let teams = groups[groupName];
        let optionsHtml = "<option value=''>-- Team Chunein --</option>";
        teams.forEach(team => {
            optionsHtml += `<option value="${team}">${team}</option>`;
        });

        team1Select.innerHTML = optionsHtml;
        team2Select.innerHTML = optionsHtml;
    }

    function savePointTableMatch() {
        let tableName = document.getElementById('ptGroupSelect').value.trim();
        let team1 = document.getElementById('ptTeam1Select').value.trim();
        let team2 = document.getElementById('ptTeam2Select').value.trim();
        let t1Score = document.getElementById('ptTeam1ScoreInput').value.trim();
        let t2Score = document.getElementById('ptTeam2ScoreInput').value.trim();
        let customNrr = document.getElementById('ptCustomNrrInput').value.trim();

        if(!tableName) {
            alert("Kripya pehle Group chunein!");
            return;
        }
        if(!team1 || !team2) {
            alert("Kripya Team 1 aur Team 2 dono chunein!");
            return;
        }
        if(team1 === team2) {
            alert("Team 1 aur Team 2 alag-alag honi chahiye!");
            return;
        }
        if(!t1Score || !t2Score) {
            alert("Dono teams ke score details bharein!");
            return;
        }

        let tables = getPointsTables();
        if(!tables[tableName]) {
            tables[tableName] = {};
        }

        let groups = getGroups();
        let groupTeams = groups[tableName] || [];
        
        groupTeams.forEach(t => {
            if(!tables[tableName][t]) {
                tables[tableName][t] = { played: 0, won: 0, lost: 0, nr: 0, nrr: '0.000', points: 0 };
            }
        });

        if(!tables[tableName][team1]) tables[tableName][team1] = { played: 0, won: 0, lost: 0, nr: 0, nrr: '0.000', points: 0 };
        if(!tables[tableName][team2]) tables[tableName][team2] = { played: 0, won: 0, lost: 0, nr: 0, nrr: '0.000', points: 0 };

        // Match increment & points calculation (ICC Formula format update)
        tables[tableName][team1].played += 1;
        tables[tableName][team2].played += 1;

        // Team 1 ko winner maan kar points update kar rahe hain (aap ise change ya match result ke hisab se set kar sakte hain)
        tables[tableName][team1].won += 1;
        tables[tableName][team1].points += 2;
        
        tables[tableName][team2].lost += 1;

        if(customNrr) {
            tables[tableName][team1].nrr = customNrr;
        }

        savePointsTables(tables);

        document.getElementById('ptTeam1ScoreInput').value = "";
        document.getElementById('ptTeam2ScoreInput').value = "";
        document.getElementById('ptCustomNrrInput').value = "";

        renderAllPointsTables();
        renderAdminPointsTablesList();
        alert("Points Table match result ke mutabiq successfully update ho gayi hai!");
    }

    window.deleteEntireTable = function(tableName) {
        if(confirm(`Kya aap poori table '${tableName}' ko delete karna chahte hain?`)) {
            let tables = getPointsTables();
            delete tables[tableName];
            savePointsTables(tables);
            renderAllPointsTables();
            renderAdminPointsTablesList();
        }
    };

    function renderAdminPointsTablesList() {
        let tables = getPointsTables();
        let container = document.getElementById('adminPtTablesList');
        let keys = Object.keys(tables);

        if(keys.length === 0) {
            container.innerHTML = "<p style='font-size:12px; color:#666;'>Abhi koi points table update nahi ki gayi hai.</p>";
            return;
        }

        let html = "<div style='font-size:12px; font-weight:bold; margin-bottom:5px;'>Update ki hui Tables (Delete Option):</div>";
        keys.forEach(tName => {
            let teamsCount = Object.keys(tables[tName]).length;
            html += `<div style="background:#fff; padding:5px 8px; border:1px solid #ccc; border-radius:4px; margin-bottom:4px; display:flex; justify-content:space-between; align-items:center;">
                <span><b>${tName}</b> (${teamsCount} Teams)</span>
                <button onclick="deleteEntireTable('${tName}')" style="background:#dc3545; color:white; border:none; padding:3px 6px; border-radius:3px; font-size:10px; cursor:pointer; width:auto;">Delete Table</button>
            </div>`;
        });
        container.innerHTML = html;
    }

    function renderAllPointsTables() {
        let tables = getPointsTables();
        let container = document.getElementById('pointsTablesDisplayContainer');
        let keys = Object.keys(tables);

        if(keys.length === 0) {
            container.innerHTML = `<div class="card"><h3>🏆 Points Table</h3><p style='font-size:13px; color:var(--text-muted); text-align:center;'>Abhi koi points table uplabdh nahi hai.</p></div>`;
            return;
        }

        let html = "";
        keys.forEach(tName => {
            let teamsObj = tables[tName];
            let teamKeys = Object.keys(teamsObj);

            // REAL ICC FORMULA SORTING: 1. Points, 2. Net Run Rate (NRR)
            teamKeys.sort((a, b) => {
                let ptsDiff = teamsObj[b].points - teamsObj[a].points;
                if(ptsDiff !== 0) return ptsDiff;
                return parseFloat(teamsObj[b].nrr || 0) - parseFloat(teamsObj[a].nrr || 0);
            });

            html += `<div class="card">
                <h3 style="color: var(--primary-dark);">🏆 ${tName}</h3>
                <table>
                    <tr><th>#</th><th style="text-align:left; padding-left:5px;">Team</th><th>P</th><th>W</th><th>L</th><th>NR</th><th>Pts</th><th>NRR</th></tr>`;
            
            let rank = 1;
            teamKeys.forEach(t => {
                let d = teamsObj[t];
                html += `<tr>
                    <td>${rank++}</td>
                    <td style="text-align:left; padding-left:5px;"><b>${t}</b></td>
                    <td>${d.played}</td>
                    <td>${d.won}</td>
                    <td>${d.lost}</td>
                    <td>${d.nr || 0}</td>
                    <td><b>${d.points}</b></td>
                    <td>${d.nrr || '0.000'}</td>
                </tr>`;
            });
            html += `</table></div>`;
        });
        container.innerHTML = html;
    }

    function addNewMatch() {
        let currentPhone = localStorage.getItem('current_user');
        let users = getUsers();
        let userData = users[currentPhone];
        let editId = document.getElementById('editMatchId').value;

        if(!editId && userData.subscription === '3 Match Subscription') {
            if(userData.matchesLeft <= 0) {
                alert("Aapka 3 match schedule karne ka quota khatam ho gaya hai! Kripya naya plan lein.");
                return;
            }
        }

        let series = document.getElementById('seriesName').value.trim();
        let seriesType = document.getElementById('seriesTypeOption').value;
        let format = document.getElementById('matchFormat').value.trim();
        let t1 = document.getElementById('team1').value.trim();
        let t2 = document.getElementById('team2').value.trim();
        let venue = document.getElementById('venue').value.trim();
        let tossUpdate = document.getElementById('matchTossUpdate').value.trim();

        if(!series || !format || !t1 || !t2) {
            alert("Sabhi zaroori fields bharein!");
            return;
        }

        let matches = getMatches();

        if(editId) {
            let match = matches.find(m => m.id == editId);
            if(match) {
                match.series = series;
                match.seriesType = seriesType;
                match.format = format;
                match.t1 = t1;
                match.t2 = t2;
                match.venue = venue;
                match.tossUpdate = tossUpdate;
            }
            alert("Match successfully update ho gaya!");
        } else {
            matches.push({ id: Date.now(), series, seriesType, format, t1, t2, venue, tossUpdate, winner: "Upcoming", t1Score: "", t2Score: "" });
            
            if(userData.subscription === '3 Match Subscription') {
                userData.matchesLeft -= 1;
                if(userData.matchesLeft <= 0) {
                    userData.subscription = null;
                }
                saveUsers(users);
            }

            alert("Match successfully schedule ho gaya!");
        }

        saveMatches(matches);
        resetMatchForm();
        loadDashboard();
    }

    function resetMatchForm() {
        document.getElementById('editMatchId').value = "";
        document.getElementById('seriesName').value = "";
        document.getElementById('seriesTypeOption').value = "same";
        document.getElementById('matchFormat').value = "";
        document.getElementById('team1').value = "";
        document.getElementById('team2').value = "";
        document.getElementById('venue').value = "";
        document.getElementById('matchTossUpdate').value = "";
        document.getElementById('saveMatchBtn').innerText = "Match Save Karein";
    }

    window.editMatch = function(id) {
        let matches = getMatches();
        let match = matches.find(m => m.id == id);
        if(match) {
            document.getElementById('editMatchId').value = match.id;
            document.getElementById('seriesName').value = match.series;
            document.getElementById('seriesTypeOption').value = match.seriesType || "same";
            document.getElementById('matchFormat').value = match.format;
            document.getElementById('team1').value = match.t1;
            document.getElementById('team2').value = match.t2;
            document.getElementById('venue').value = match.venue;
            document.getElementById('matchTossUpdate').value = match.tossUpdate || "";
            
            document.getElementById('saveMatchBtn').innerText = "Update Karein";
            
            document.getElementById('adminPanelSection').classList.remove('hidden');
            window.scrollTo({ top: 0, behavior: 'smooth' });
        }
    };

    window.deleteMatch = function(id) {
        if(confirm("Kya aap sach mein is match ko delete karna chahte hain?")) {
            let matches = getMatches();
            matches = matches.filter(m => m.id != id);
            saveMatches(matches);
            loadDashboard();
            alert("Match delete kar diya gaya hai.");
        }
    };

    function renderSchedule() {
        let matches = getMatches();
        let container = document.getElementById('scheduleList');
        let showAdminControls = isAdminUnlocked;

        if(matches.length === 0) {
            container.innerHTML = "<p style='font-size:13px; color:var(--text-muted); text-align:center;'>Abhi koi match schedule nahi hai.</p>";
            return;
        }

        let html = "";
        let currentSeries = "";

        matches.forEach((m) => {
            if(m.series !== currentSeries) {
                currentSeries = m.series;
                let gapClass = (m.seriesType === 'new') ? 'with-gap' : 'no-gap';
                html += `<div class="series-title ${gapClass}">📌 ${currentSeries}</div>`;
            }
            html += `<div class="match-box">
                <div class="match-info-top">
                    <span>${m.format}</span>
                    <span>📍 ${m.venue}</span>
                </div>
                <div class="match-teams">
                    <span>🏏 ${m.t1} <span style="font-size:12px; color:#555;">${m.t1Score}</span></span>
                    <span>vs</span>
                    <span>${m.t2} 🏏 <span style="font-size:12px; color:#555;">${m.t2Score}</span></span>
                </div>`;
            
            if(m.tossUpdate) {
                html += `<div class="match-toss-banner">ℹ️ ${m.tossUpdate}</div>`;
            }

            if(m.winner && m.winner !== "Upcoming") {
                html += `<div class="match-result-banner">🏆 ${m.winner}</div>`;
            }

            if(showAdminControls) {
                html += `<div style="margin-top:8px; display:flex; gap:5px;">
                    <button onclick="editMatch(${m.id})" style="background:#0284c7; color:white; border:none; padding:5px; border-radius:4px; font-size:12px; cursor:pointer; flex:1;">Edit Match</button>
                    <button onclick="deleteMatch(${m.id})" style="background:#dc3545; color:white; border:none; padding:5px; border-radius:4px; font-size:12px; cursor:pointer; flex:1;">Delete Match</button>
                </div>`;
            }
            html += `</div>`;
        });
        container.innerHTML = html;
    }

    function updateMatchDropdown() {
        let matches = getMatches();
        let select = document.getElementById('matchSelectForUpdate');
        select.innerHTML = "<option value=''>Match Chunein update karne ke liye</option>";
        matches.forEach((m) => {
            select.innerHTML += `<option value="${m.id}">${m.series} - ${m.t1} vs ${m.t2} (${m.format})</option>`;
        });
    }

    function updateMatchResult() {
        let matchId = document.getElementById('matchSelectForUpdate').value;
        let winner = document.getElementById('matchWinner').value.trim();
        let t1Score = document.getElementById('team1ScoreDetails').value.trim();
        let t2Score = document.getElementById('team2ScoreDetails').value.trim();

        if(!matchId) {
            alert("Kripya match chunein!");
            return;
        }

        let matches = getMatches();
        let match = matches.find(m => m.id == matchId);
        if(match) {
            match.winner = winner || match.winner;
            match.t1Score = t1Score || match.t1Score;
            match.t2Score = t2Score || match.t2Score;
            saveMatches(matches);
            alert("Match Result update ho gaya!");
            loadDashboard();
        }
    }

    function createGroup() {
        let gName = document.getElementById('groupNameInput').value.trim();
        let teamsInput = document.getElementById('groupTeamsInput').value.trim();

        if(!gName || !teamsInput) {
            alert("Group name aur teams dalein!");
            return;
        }

        let groups = getGroups();
        let teamsArr = teamsInput.split(',').map(t => t.trim());
        groups[gName] = teamsArr;
        saveGroups(groups);

        alert("Group successfully ban gaya!");
        document.getElementById('groupNameInput').value = "";
        document.getElementById('groupTeamsInput').value = "";
        renderGroups();
        populateAdminGroupDropdown();
        renderAdminGroupsList();
    }

    window.deleteGroup = function(groupName) {
        if(confirm(`Kya aap group '${groupName}' ko delete karna chahte hain?`)) {
            let groups = getGroups();
            delete groups[groupName];
            saveGroups(groups);
            renderGroups();
            populateAdminGroupDropdown();
            renderAdminGroupsList();
        }
    }

    function renderGroups() {
        let groups = getGroups();
        let container = document.getElementById('groupsContainer');
        let keys = Object.keys(groups);

        if(keys.length === 0) {
            container.innerHTML = "<p style='font-size:13px; color:var(--text-muted);'>Abhi koi group nahi banaya gaya hai.</p>";
            return;
        }

        let html = "";
        keys.forEach(g => {
            html += `<div style="background:#f9f9f9; border:1px solid #ddd; padding:8px; border-radius:6px; margin-bottom:8px;">
                <div><strong>📌 ${g}</strong><br><span style="font-size:13px; color:#555;">Teams: ${groups[g].join(', ')}</span></div>
            </div>`;
        });
        container.innerHTML = html;
    }

    function renderAdminGroupsList() {
        let groups = getGroups();
        let container = document.getElementById('adminGroupsList');
        let keys = Object.keys(groups);

        if(keys.length === 0) {
            container.innerHTML = "<p style='font-size:12px; color:#666; margin-top:5px;'>Abhi koi group nahi hai.</p>";
            return;
        }

        let html = "<div style='font-size:12px; font-weight:bold; margin-top:8px;'>Bane hue Groups (Delete Option):</div>";
        keys.forEach(g => {
            html += `<div style="background:#fff; padding:5px 8px; border:1px solid #ccc; border-radius:4px; margin-top:4px; display:flex; justify-content:space-between; align-items:center;">
                <span style="font-size:13px;"><b>${g}</b> (${groups[g].length} Teams)</span>
                <button onclick="deleteGroup('${g}')" style="background:#dc3545; color:white; border:none; padding:3px 6px; border-radius:3px; font-size:10px; cursor:pointer; width:auto;">Delete Group</button>
            </div>`;
        });
        container.innerHTML = html;
    }

    function logoutUser() {
        let currentPhone = localStorage.getItem('current_user');
        if(currentPhone) {
            let activeSessions = JSON.parse(localStorage.getItem('active_sessions')) || {};
            delete activeSessions[activeSessions];
            localStorage.setItem('active_sessions', JSON.stringify(activeSessions));
        }

        isAdminUnlocked = false;
        localStorage.removeItem('current_user');
        document.getElementById('dashboardSection').classList.add('hidden');
        document.getElementById('appTabs').classList.add('hidden');
        document.getElementById('loginSection').classList.remove('hidden');
        document.getElementById('userPhoneInput').value = "";
        resetLogin();
    }

    document.addEventListener('DOMContentLoaded', function() {
        document.getElementById('adminBtn').addEventListener('click', checkAdminAccess);
        document.getElementById('sendOtpBtn').addEventListener('click', sendOTP);
        document.getElementById('verifyOtpBtn').addEventListener('click', verifyOTP);
        document.getElementById('resetLoginBtn').addEventListener('click', resetLogin);
        document.getElementById('createGroupBtn').addEventListener('click', createGroup);
        document.getElementById('redeemCodeBtn').addEventListener('click', redeemPointsCode);
        document.getElementById('generateCodeBtn').addEventListener('click', generateRedeemCode);
        document.getElementById('saveMatchBtn').addEventListener('click', addNewMatch);
        document.getElementById('updateResultBtn').addEventListener('click', updateMatchResult);
        document.getElementById('savePointTableMatchBtn').addEventListener('click', savePointTableMatch);
        document.getElementById('closeAdminBtn').addEventListener('click', closeAdminPanel);
        document.getElementById('logoutBtn').addEventListener('click', logoutUser);
        
        document.getElementById('ptGroupSelect').addEventListener('change', onAdminGroupSelected);

        document.querySelectorAll('.tab-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                switchTab(this.getAttribute('data-tab'));
            });
        });

        document.querySelectorAll('.buy-sub-btn').forEach(btn => {
            btn.addEventListener('click', function() {
                buySubscription(parseInt(this.getAttribute('data-cost')), this.getAttribute('data-plan'));
            });
        });

        if(localStorage.getItem('current_user')) {
            loadDashboard();
        }
    });
</script>

</body>
</html>
