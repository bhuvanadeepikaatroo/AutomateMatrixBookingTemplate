# Personal Setup Guide for Matrix Booking Automation

## 🎯 Quick Setup Checklist

### 1. Repository Setup
- [x] ✅ GitHub Actions workflows created
- [x] ✅ Timezone configuration updated
- [ ] 🔄 Configure repository secrets (see below)
- [ ] 🔄 Test the automation

### 2. Required Repository Secrets

Go to your GitHub repository → **Settings** → **Secrets and variables** → **Actions** → **New repository secret**

#### Essential Secrets (Required):
1. **`AUTOBOOKING_DESK_ID`**
   - Your specific desk/seat ID from Matrix Booking
   - Example: `3058825798`
   - How to find: Follow steps in "Getting Your Secrets" section below

2. **`AUTOBOOKING_SESSION_COOKIE`**
   - Your authentication cookie from Matrix Booking website
   - ⚠️ **Important**: This expires every ~3 weeks, so you'll need to update it regularly
   - How to find: Follow steps in "Getting Your Secrets" section below

**Note**: Timezone is configured for Asia/Calcutta (India Standard Time)

#### Optional Secrets (For Telegram Notifications):
4. **`AUTOBOOKING_TELEGRAM_BOT_TOKEN`**
   - Get from @BotFather on Telegram using `/newbot` command
   
5. **`AUTOBOOKING_TELEGRAM_CHAT_ID`**
   - Your Telegram user ID (get from @userinfobot)
   - ⚠️ **Important**: Send a message to your bot first!

### 3. Getting Your Secrets from Matrix Booking

1. **Open Matrix Booking website** in your browser
2. **Open Developer Tools** (F12 or Cmd+Option+I on Mac)
3. **Go to Network tab** in Developer Tools
4. **Navigate to booking page** and click on your desired seat
5. **Look for network requests** - you'll see API calls
6. **Click on a booking-related request** to see details
7. **Copy the values**:
   - `DESK_ID`: Look for `locationId` in the request payload
   - `SESSION_COOKIE`: Copy the entire `Cookie` header value

### 4. Schedule Configuration

The automation runs:
- **Create Booking**: Daily at 12:00 AM (midnight) - books 8 days ahead
- **Check-in**: Daily at 9:00 AM - checks in for today's booking
- **Days**: Monday through Friday only (weekends skipped)

**Note**: GitHub Actions uses UTC time, so the actual run times depend on your timezone setting.

### 5. Testing Your Setup

1. **Manual Test**: Go to Actions tab → Select "Create Booking" or "Check-in" → "Run workflow"
2. **Check logs**: Review the workflow run logs for any errors
3. **Verify booking**: Check Matrix Booking website to confirm booking was created

### 6. Maintenance

- **Update session cookie** every 3 weeks when it expires
- **Monitor Telegram notifications** (if configured) for status updates
- **Manually book** for the next 7 days initially (automation books 8 days ahead)

### 7. Troubleshooting

**Common Issues**:
- **401 Unauthorized**: Session cookie expired → Update `AUTOBOOKING_SESSION_COOKIE`
- **No eligible booking**: No booking exists for check-in → Verify booking was created
- **Timezone issues**: Bookings at wrong time → Check `AUTOBOOKING_TIMEZONE` setting

**Getting Help**:
- Check workflow logs in GitHub Actions tab
- Telegram notifications (if configured) provide real-time status
- Review the original README.md for additional details

---

## 🚀 You're All Set!

Once you've configured the secrets, your Matrix Booking automation will:
1. Automatically book your desk 8 days in advance every weekday at midnight
2. Automatically check you in every weekday at 9 AM
3. Send you Telegram notifications about the status (if configured)
4. Skip weekends automatically

Remember to manually book for the next 7 days initially since the automation starts booking 8 days ahead!
