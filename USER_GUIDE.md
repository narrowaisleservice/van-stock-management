# Van Stock Management System - User Guide

## For Engineers 🔧

### Logging In
1. Open the Van Stock app on your tablet
2. Select your name from the dropdown
3. Enter your 4-digit PIN code
4. Click **Login**

**First time?** Your default PIN is `1234` - please change it!

---

### My Van Stock View

After logging in, you'll see your van's current stock levels.

#### Understanding the Display

**Stats Cards** (top of page):
- **Van Number** - Your assigned van
- **Total Parts** - Total quantity of all parts
- **Low Stock Items** - Parts below minimum level (need replenishment)
- **Stock Value** - Total value of stock in your van

#### Stock Table

Each part shows:
- **Part Number** - Unique identifier
- **Description** - What the part is
- **Quantity** - Current stock with +/- buttons
- **Min / Max** - Target stock levels
- **Actions** - Save button
- **Status** - Stock level indicator:
  - 🟢 **OK** - Within min/max range
  - 🔴 **Need Replen** - Below minimum (needs restocking)
  - 🟠 **Overstocked** - Above maximum

---

### Updating Stock Quantities

#### When to Update
- ✅ After using parts on a job
- ✅ After receiving replenishment stock
- ✅ During weekly stock checks
- ✅ If you find discrepancies

#### How to Update
1. Find the part in the table
2. Use **-** button to decrease quantity
3. Use **+** button to increase quantity
4. Click **Save** button to save changes
5. Wait for "Updated successfully!" message

**Important**: Changes are saved to the central database immediately. Make sure the quantity is correct before clicking Save!

---

### My Replenishment List

Click the **My Replen List** tab to see parts that need replenishment.

#### What You'll See
- Parts currently below minimum level
- How many you need to bring stock back to maximum
- Current quantity vs required quantity

#### What to Do
1. Review the list
2. Request parts from stock manager
3. When received, update quantities in "My Van Stock" tab

---

### Search Function

Use the search bar to quickly find parts:
- Search by part number
- Search by description
- Search is instant - just start typing!

---

### Best Practices

#### Daily
- Update stock after each job if parts used
- Check for low stock warnings

#### Weekly
- Review full stock list
- Check replenishment needs
- Report any issues to stock manager

#### Monthly
- Verify all quantities are accurate
- Check for obsolete/unused parts

---

### Tips for Tablet Use

✅ **Do:**
- Keep tablet charged
- Use in landscape mode for better view
- Save changes frequently
- Log out when finished

❌ **Don't:**
- Share your PIN code
- Let others update your van stock
- Forget to save changes
- Use when signal is poor (wait for better connection)

---

### Troubleshooting

#### "Connection error" message
- Check tablet has internet connection
- Try refreshing the page
- Contact IT if problem persists

#### Can't find a part
- Use search function
- Check spelling
- Contact stock manager if part is missing

#### Quantity won't save
- Check internet connection
- Try logging out and back in
- Contact IT support

#### Forgot PIN
- Contact your manager or IT support
- They can reset it for you

---

## For Management 📊

### Logging In
1. Open the Van Stock app
2. Select "Management"
3. Enter management PIN
4. Click **Login**

---

### Dashboard View

See overview of entire fleet:

**Summary Stats:**
- Total Vans - Number of active vans
- Total Parts - Combined quantity across all vans
- Low Stock Items - Parts below minimum across fleet
- Total Stock Value - Combined value of all van stock

**Van Selector:**
- Click any van card to see detailed stock
- Shows part count and value per van

---

### All Vans View

#### Viewing a Van
1. Click on van card in dashboard
2. See complete stock list for that van
3. Use search to find specific parts
4. Click "Back to Dashboard" to return

#### What You Can See
- All parts in the van
- Current quantities
- Min/Max levels
- Stock status (Low/OK/High)
- Unit prices
- Total values

---

### Replenishment Management

Click **Replenishment** tab to see all parts needing replenishment across entire fleet.

#### Features
- See all vans with low stock items
- Sort by van, part, or quantity needed
- Export list to Excel
- Print pick list

#### Creating Pick Lists
1. Go to Replenishment tab
2. Review list of low stock items
3. Click **Export to Excel**
4. Use exported file to pick parts from stores
5. Distribute to vans
6. Engineers update their quantities when received

---

### Stock Audit

Click **Stock Audit** tab to export current stock data.

#### Running an Audit
1. Select van (or "All Vans")
2. Click **Export Audit to Excel**
3. CSV file downloads automatically

#### Audit File Contains
- Van number
- Part numbers and descriptions
- Current quantities
- Unit prices
- Total values
- Summary totals
- Audit date/time

#### When to Run Audits
- Monthly stock checks
- Before financial year end
- When investigating discrepancies
- For insurance purposes

---

### Fleet Management Tips

#### Weekly Tasks
- Review replenishment lists
- Check for persistent low stock items
- Monitor high-value items
- Ensure engineers are updating regularly

#### Monthly Tasks
- Run full fleet audit
- Export for accounting
- Review min/max levels
- Check for trends

#### Ad-Hoc Tasks
- Investigate stock discrepancies
- Add new parts to system
- Remove obsolete parts
- Update pricing

---

### Understanding Stock Levels

**Setting Min/Max:**
- **Min** - Reorder point (when to replenish)
- **Max** - Target stock level (after replenishment)

**Guidelines:**
- Fast-moving parts: Higher min/max
- Slow-moving parts: Lower min/max
- Expensive parts: Lower max
- Critical parts: Higher min

**Adjusting Levels:**
- Update in Google Sheets VanInventory tab
- Or adjust in StockMaster for all vans
- Review quarterly based on usage

---

### Reports You Can Generate

#### Replenishment Lists
- Who needs what
- Quantities required
- By van or fleet-wide

#### Stock Audits
- Current stock snapshot
- Values and quantities
- By van or fleet-wide

#### Custom Analysis
- Export to Excel
- Use pivot tables
- Analyze trends
- Identify issues

---

### System Administration

#### Managing Users
1. Open Google Sheet
2. Go to "Users" tab
3. Add/edit/remove engineers
4. Assign van numbers
5. Reset PINs if needed

#### Managing Stock Master
1. Open Google Sheet
2. Go to "StockMaster" tab
3. Add new parts
4. Update prices
5. Set standard min/max

#### Backup Procedures
- Weekly: Download Google Sheet as Excel
- Monthly: Full backup of all data
- Store backups securely

---

### Security Best Practices

✅ **Do:**
- Protect management PIN
- Regular backups
- Review access logs
- Update PINs quarterly

❌ **Don't:**
- Share management access
- Leave logged in unattended
- Skip regular audits
- Ignore discrepancies

---

### Getting Help

**Technical Issues:**
- Check SETUP.md for troubleshooting
- Review Apps Script logs
- Check Google Sheet data integrity
- Contact IT support

**Stock Issues:**
- Investigate in Google Sheet directly
- Check LastModified timestamps
- Review engineer usage patterns
- Discuss with affected engineer

**Feature Requests:**
- Document requirement
- Discuss with IT
- Consider impact on all users
- Plan implementation

---

## Quick Reference

### Common Tasks

| Task | Engineer | Management |
|------|----------|------------|
| Update stock quantity | ✅ My Van only | ✅ View only |
| View replen list | ✅ My Van only | ✅ All vans |
| Export audit | ❌ | ✅ |
| Change PIN | ✅ | ✅ |
| Add parts | ❌ | ✅ Via Sheet |
| View all vans | ❌ | ✅ |

### Status Indicators

| Color | Status | Meaning | Action |
|-------|--------|---------|--------|
| 🟢 Green | OK | Within range | None |
| 🔴 Red | Low | Below min | Replenish |
| 🟠 Orange | High | Above max | Review |

### Contact Information

- **Stock Manager**: [Your Contact]
- **IT Support**: [IT Contact]
- **Emergency**: [Emergency Contact]

---

*Last updated: December 2024*
*Version: 1.0*
