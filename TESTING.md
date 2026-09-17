# KisanSetu - Complete Testing Guide

## Pre-Testing Checklist

Before starting tests, ensure:
- [ ] MongoDB is running
- [ ] Demo data is seeded (`cd backend && npm run seed`)
- [ ] Backend server is running on port 5000
- [ ] Frontend is running on port 5173
- [ ] Both terminals show no errors

## Test Suite 1: Authentication & Authorization

### Test 1.1: Farmer Registration
**Steps:**
1. Open http://localhost:5173
2. Click "Register"
3. Fill form:
   - Name: Test Farmer
   - Email: test@farmer.com
   - Phone: 9999999999
   - Password: test123
   - Role: Farmer
   - Village: Test Village
4. Click "Sign Up"

**Expected:**
- ✓ Success message appears
- ✓ Redirects to farmer dashboard
- ✓ User is logged in

### Test 1.2: Farmer Login
**Steps:**
1. Logout if logged in
2. Click "Demo Farmer" button OR enter: ramesh@demo.com / demo123
3. Click "Sign In"

**Expected:**
- ✓ Success message
- ✓ Redirects to /dashboard
- ✓ Dashboard shows active token K-001
- ✓ User name "Ramesh Kumar" appears in navbar

### Test 1.3: Admin Login
**Steps:**
1. Logout
2. Click "Demo Admin" button OR enter: admin@demo.com / admin123
3. Click "Sign In"

**Expected:**
- ✓ Redirects to /admin
- ✓ Shows admin dashboard with statistics
- ✓ Shows list of mandis

### Test 1.4: Authorization Check
**Steps:**
1. Login as farmer
2. Try to access: http://localhost:5173/admin

**Expected:**
- ✓ Redirects to home page (unauthorized)

---

## Test Suite 2: Farmer Dashboard & Queue Tracking

### Test 2.1: Dashboard Data Display
**Login as:** ramesh@demo.com / demo123

**Verify Dashboard Shows:**
- ✓ Token number: K-001
- ✓ Queue position (should be 1-3)
- ✓ Estimated wait time (in minutes)
- ✓ Expected turn time
- ✓ Farmers ahead count
- ✓ Farmers completed count
- ✓ Mandi name: Meerut Mandi / मेरठ मंडी
- ✓ Crop details: Wheat, 50 quintal
- ✓ Status badge showing current status

### Test 2.2: Live Queue View
**Steps:**
1. From dashboard, click "View Queue"
2. Observe queue information

**Expected:**
- ✓ Shows current position
- ✓ Shows farmers ahead
- ✓ Live updates indicator (green pulse)
- ✓ All data matches dashboard

### Test 2.3: Delay Analysis
**Steps:**
1. From dashboard, click "Why is my procurement delayed?"
2. Read analysis

**Expected:**
- ✓ Shows summary in English or Hindi based on language setting
- ✓ Lists specific delay reasons
- ✓ Shows factors like: queue ahead, limited counters, processing time
- ✓ Information is logical and accurate

---

## Test Suite 3: Real-Time Updates (CRITICAL)

### Test 3.1: Admin Changes Status → Farmer Sees Update
**Setup:**
1. Open two browser windows (or use incognito for second)
2. Window 1: Login as farmer (ramesh@demo.com)
3. Window 2: Login as admin (admin@demo.com)

**Steps:**
1. Admin: Navigate to Queue Management for Meerut Mandi
2. Admin: Find token K-001, change status dropdown to "Quality Check"
3. Switch to Farmer window
4. Observe dashboard

**Expected:**
- ✓ Farmer dashboard updates within 2-3 seconds
- ✓ Status badge changes to "Quality Check"
- ✓ Toast notification appears
- ✓ No page refresh needed

### Test 3.2: Admin Calls Next → Queue Updates
**Setup:**
1. Keep both windows open from Test 3.1
2. Farmer should be on dashboard or queue view

**Steps:**
1. Admin: Click "Call Next" button
2. Wait for confirmation
3. Check farmer window

**Expected:**
- ✓ Farmer sees queue position change
- ✓ Farmers ahead count decreases
- ✓ Estimated wait time recalculates
- ✓ If farmer's turn: Big notification appears

---

## Test Suite 4: Mandi Discovery & Booking

### Test 4.1: Explore Mandis
**Login as:** vijay@demo.com / demo123

**Steps:**
1. Click "Mandis" in navigation
2. Browse mandi cards
3. Use search: type "Meerut"

**Expected:**
- ✓ Shows 3 mandis (Meerut, Hapur, Ghaziabad)
- ✓ Each card shows: name, location, rating, operating hours, active counters
- ✓ Search filters correctly
- ✓ All cards have "View Details" button

### Test 4.2: View Mandi Details
**Steps:**
1. From mandis page, click "View Details" on any mandi
2. Review information

**Expected:**
- ✓ Shows complete mandi information
- ✓ Operating hours displayed
- ✓ Current queue length shown
- ✓ Completed today count shown
- ✓ "Book Slot" button visible

### Test 4.3: Complete Booking Flow
**Steps:**
1. From mandi details, click "Book Slot"
2. Select date: Tomorrow or any future date
3. Wait for time slots to load
4. Select a time slot (e.g., 09:00)
5. Fill form:
   - Crop Type: Rice
   - Quantity: 40
   - Unit: quintal
   - Estimated Value: 80000
6. Click "Confirm Booking"

**Expected:**
- ✓ Time slots appear after selecting date
- ✓ Available slots are clickable
- ✓ Form validation works
- ✓ Success message appears
- ✓ Redirects to dashboard
- ✓ New token visible on dashboard
- ✓ Notification created

---

## Test Suite 5: Multilingual Support

### Test 5.1: Language Switch
**Steps:**
1. Login as any user
2. Click language icon (EN) in navbar
3. Select Hindi
4. Navigate through pages

**Expected:**
- ✓ Navbar items change to Hindi
- ✓ Dashboard labels in Hindi
- ✓ Buttons in Hindi
- ✓ Notifications in Hindi
- ✓ Status labels in Hindi
- ✓ Mandi names show Hindi version where available
- ✓ All major UI text translated

### Test 5.2: Notification Language
**Steps:**
1. Set language to Hindi
2. Check notifications page
3. Switch to English
4. Check again

**Expected:**
- ✓ Notifications show in Hindi when language is Hindi
- ✓ Notifications show in English when language is English
- ✓ Both versions available for each notification

---

## Test Suite 6: Voice Assistant

### Test 6.1: Voice Recognition (Chrome/Edge only)
**Login as:** ramesh@demo.com / demo123

**Steps:**
1. Navigate to Voice Assistant page
2. Click microphone button
3. Say: "What is my token?"
4. Wait for response

**Expected:**
- ✓ Microphone activates (button turns red, shows "Listening...")
- ✓ Transcription appears after speaking
- ✓ Response appears with token number
- ✓ Text-to-speech plays response (if supported)

### Test 6.2: Voice Commands
**Test each command:**
1. "What is my token?" → Should say "K-001"
2. "How many farmers are ahead?" → Should give count
3. "When is my turn?" → Should give estimated time
4. "Why is my procurement delayed?" → Should explain reasons

**Expected:**
- ✓ Each command understood correctly
- ✓ Relevant response provided
- ✓ Hindi commands work if language is Hindi

### Test 6.3: Fallback for Unsupported Browsers
**Steps:**
1. Try in Firefox (voice API not supported)
2. Click microphone

**Expected:**
- ✓ Shows message: "Voice recognition not supported"
- ✓ Suggests using text input
- ✓ No crashes or errors

---

## Test Suite 7: Admin Portal

### Test 7.1: Admin Dashboard
**Login as:** admin@demo.com / admin123

**Verify Dashboard Shows:**
- ✓ Total Tokens count (should be 8+)
- ✓ Completed Tokens count
- ✓ Active Tokens count
- ✓ Average Wait Time
- ✓ All stats are numbers (not null/undefined)
- ✓ List of mandis with queue info

### Test 7.2: Queue Management
**Steps:**
1. Click "Queue Management" on Meerut Mandi card
2. Review queue

**Expected:**
- ✓ Shows current token being processed
- ✓ Shows counter number
- ✓ Lists all active tokens in queue
- ✓ Each token shows: number, farmer name, phone, crop, quantity
- ✓ Status dropdown for each token
- ✓ "Call Next" button visible

### Test 7.3: Call Next Farmer
**Steps:**
1. In queue management, click "Call Next"
2. Wait for confirmation
3. Check queue

**Expected:**
- ✓ Success toast appears
- ✓ Next token moves to "Current Token" section
- ✓ Token status changes to "Verification"
- ✓ Queue list updates
- ✓ Stats update (active/completed counts)

### Test 7.4: Update Token Status
**Steps:**
1. Find any active token in queue
2. Change status dropdown: Verification → Quality Check
3. Change again: Quality Check → Procurement
4. Finally: Procurement → Completed

**Expected:**
- ✓ Each change shows success message
- ✓ Status badge updates immediately
- ✓ If set to "Completed": token removed from active queue
- ✓ Completed count increases

### Test 7.5: Status Progression
**Steps:**
1. Take one token through complete lifecycle:
   - Booked → Arrived → Verification → Quality Check → Procurement → Payment Pending → Completed

**Expected:**
- ✓ All status changes work
- ✓ Farmer receives notifications for each change
- ✓ Queue position updates for other farmers
- ✓ Stats update correctly

---

## Test Suite 8: Notifications

### Test 8.1: View Notifications
**Login as:** any farmer

**Steps:**
1. Click bell icon in navbar
2. View notification list

**Expected:**
- ✓ Shows list of notifications
- ✓ Unread notifications highlighted
- ✓ Each shows: title, message, time ago
- ✓ Recent notifications at top

### Test 8.2: Mark as Read
**Steps:**
1. Click checkmark on unread notification
2. Observe changes

**Expected:**
- ✓ Notification background changes (no longer highlighted)
- ✓ Unread count decreases
- ✓ Checkmark button disappears

### Test 8.3: Real-Time Notification
**Setup:**
1. Farmer window: Open notifications page
2. Admin window: Change farmer's token status

**Expected:**
- ✓ New notification appears in list without refresh
- ✓ Unread count increases

---

## Test Suite 9: Responsive Design

### Test 9.1: Mobile View (400px width)
**Steps:**
1. Open DevTools (F12)
2. Toggle device toolbar
3. Select iPhone SE or custom 400px width
4. Navigate through all pages

**Expected:**
- ✓ Navigation hamburger menu works
- ✓ All cards stack vertically
- ✓ Text remains readable
- ✓ Buttons are clickable
- ✓ Forms are usable
- ✓ No horizontal scroll

### Test 9.2: Tablet View (768px width)
**Expected:**
- ✓ 2-column layouts work
- ✓ Navigation shows key items
- ✓ Dashboard cards arrange properly

---

## Test Suite 10: 3D Graphics & Animations

### Test 10.1: Landing Page Hero
**Steps:**
1. Logout (or open incognito)
2. Visit homepage
3. Observe 3D scene

**Expected:**
- ✓ Floating 3D spheres visible
- ✓ Spheres rotate and move
- ✓ Colors: green shades
- ✓ No lag or freezing
- ✓ Scene loads within 2-3 seconds

### Test 10.2: Framer Motion Animations
**Check these animations:**
1. Page transitions (login → dashboard)
2. Card hover effects (mandi cards lift on hover)
3. Button scale on click
4. Notification slide-in
5. Dashboard data fade-in
6. Scroll animations on landing page

**Expected:**
- ✓ All animations smooth (60fps)
- ✓ No janky movements
- ✓ Hover effects respond immediately

---

## Test Suite 11: Error Handling

### Test 11.1: Invalid Login
**Steps:**
1. Try login with: wrong@email.com / wrongpass

**Expected:**
- ✓ Error message appears
- ✓ Doesn't crash
- ✓ Form remains usable

### Test 11.2: Network Error Simulation
**Steps:**
1. Login successfully
2. Stop backend server
3. Try to book a slot or change status

**Expected:**
- ✓ Error toast appears
- ✓ App doesn't crash
- ✓ User can retry after backend restarts

### Test 11.3: Duplicate Booking Prevention
**Steps:**
1. Login as farmer with active token
2. Try to book another slot for same date

**Expected:**
- ✓ Error message: "Already have active token"
- ✓ Booking prevented

---

## Test Suite 12: Data Persistence

### Test 12.1: Logout & Login
**Steps:**
1. Login as farmer
2. Note queue position and data
3. Logout
4. Login again as same farmer

**Expected:**
- ✓ Same token visible
- ✓ Queue position maintained
- ✓ All data intact

### Test 12.2: Browser Refresh
**Steps:**
1. Login and navigate to any page
2. Refresh browser (F5)

**Expected:**
- ✓ Remains logged in
- ✓ Same page loads
- ✓ Data intact
- ✓ Language preference maintained

---

## Test Suite 13: My Tokens History

### Test 13.1: View All Tokens
**Login as:** ramesh@demo.com

**Steps:**
1. Navigate to "My Tokens"
2. Review list

**Expected:**
- ✓ Shows current active token
- ✓ Shows completed tokens (if any)
- ✓ Each token card shows: number, mandi, date, crop, quantity, status
- ✓ Active tokens have "View Queue" link

---

## Test Suite 14: Complete End-to-End Journey

### Scenario: Farmer Books Slot → Admin Processes → Completion

**Part A: Farmer Books Slot**
1. Register new farmer: newfarmer@test.com / test123
2. Navigate to Mandis
3. Select "Ghaziabad Mandi"
4. Book slot for tomorrow, 10:00 AM
5. Enter: Wheat, 60 quintal, 120000
6. Confirm booking
7. Note token number (e.g., K-123)

**Verify:**
- ✓ Token appears on dashboard
- ✓ Queue position shown
- ✓ Notification received

**Part B: Admin Processes Token**
1. Login as admin in another window
2. Go to Ghaziabad Mandi queue management
3. Find the new farmer's token
4. Call Next (if needed, process until this token is next)
5. Change status: Booked → Arrived
6. Wait 5 seconds
7. Change status: Arrived → Verification
8. Wait 5 seconds
9. Change status: Verification → Quality Check
10. Wait 5 seconds
11. Change status: Quality Check → Procurement
12. Wait 5 seconds
13. Change status: Procurement → Payment Pending
14. Wait 5 seconds
15. Change status: Payment Pending → Completed

**Verify at Each Step:**
- ✓ Farmer window shows status update (toast notification)
- ✓ Dashboard updates in real-time
- ✓ Notification created for each status change

**Part C: Completion**
1. Check farmer's dashboard
2. Check My Tokens page
3. Check Notifications

**Final Verification:**
- ✓ Token status shows "Completed"
- ✓ Token no longer shows as "active" on dashboard
- ✓ Token appears in My Tokens with completed status
- ✓ Multiple notifications received throughout process
- ✓ Admin dashboard stats updated (completed count increased)

---

## Performance Benchmarks

### Target Metrics:
- [ ] Page load time: < 2 seconds
- [ ] API response time: < 500ms
- [ ] Socket connection: < 1 second
- [ ] Real-time update delay: < 3 seconds
- [ ] 3D scene load: < 3 seconds

### Tools to Test:
1. Chrome DevTools → Network tab (check load times)
2. Chrome DevTools → Performance tab (check FPS)
3. Lighthouse audit (aim for 80+ performance score)

---

## Browser Compatibility

Test in:
- [ ] Chrome (latest) - FULL SUPPORT
- [ ] Edge (latest) - FULL SUPPORT
- [ ] Firefox (latest) - VOICE ASSISTANT LIMITED
- [ ] Safari (latest) - CHECK 3D PERFORMANCE

---

## Known Limitations & Workarounds

### 1. Voice Assistant in Firefox
**Issue:** Speech Recognition API not supported
**Workaround:** App shows message and suggests text input

### 2. 3D Graphics on Low-End Devices
**Issue:** May lag or stutter
**Workaround:** 3D is only on homepage (optional)

### 3. Socket Disconnection
**Issue:** If socket connection fails
**Workaround:** App falls back to polling API every 30 seconds

### 4. MongoDB Not Running
**Issue:** Backend fails to start
**Solution:** Start MongoDB first: `mongod`

---

## Success Criteria

The application passes testing if:

✓ **Authentication**: Login/logout/register all work
✓ **Authorization**: Role-based access enforced
✓ **Real-time**: Socket updates work within 3 seconds
✓ **Booking**: Complete booking flow works
✓ **Admin**: Queue management and status updates work
✓ **Notifications**: Created and displayed correctly
✓ **Multilingual**: English/Hindi switch works
✓ **Voice**: Works in supported browsers with fallback
✓ **3D**: Renders without errors
✓ **Animations**: Smooth and performant
✓ **Responsive**: Works on mobile/tablet/desktop
✓ **End-to-End**: Complete journey from booking to completion works
✓ **No Crashes**: App handles errors gracefully
✓ **Data Integrity**: All data persists correctly

---

## Bug Reporting Template

If you find issues:

```
**Bug Title:** Brief description
**Steps to Reproduce:**
1. Step one
2. Step two
**Expected Behavior:** What should happen
**Actual Behavior:** What actually happened
**Browser:** Chrome 120 / Firefox 121 / etc.
**Screenshots:** (if applicable)
**Console Errors:** (check F12 → Console)
```

---

## Final Checklist Before Demo

- [ ] MongoDB running
- [ ] Backend running (no errors in terminal)
- [ ] Frontend running (no errors in terminal)
- [ ] Demo data seeded
- [ ] Test farmer login works
- [ ] Test admin login works
- [ ] Real-time updates work
- [ ] Voice assistant tested
- [ ] Language switch works
- [ ] Mobile view checked
- [ ] No console errors in browser

---

**Testing Complete! 🎉**

If all tests pass, the application is ready for demonstration and deployment.
