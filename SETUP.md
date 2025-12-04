# Van Stock Management System - Setup Guide

## System Overview
Comprehensive van stock management system for 15 service vans with:
- Real-time stock tracking
- Min/Max replenishment alerts
- Stock audit exports
- Engineer tablet access
- Management dashboard

## Components
1. **Google Sheets** - Central database
2. **Google Apps Script** - Backend API
3. **HTML/JavaScript Frontend** - User interface (Duda or GitHub Pages)

---

## STEP 1: Create Google Sheet

1. Go to Google Sheets: https://sheets.google.com
2. Create new spreadsheet named: **Van Stock Management**
3. Create 3 sheets with these exact names:
   - `Users`
   - `VanInventory`
   - `StockMaster`

---

## STEP 2: Setup Users Sheet

In the **Users** sheet, add these columns (Row 1):
```
Engineer | PIN | Role | VanNumber
```

Then add these users (default PIN: 1234 for all):
```
Aaron Dyson      | 1234 | Engineer | 1
Brett Stockton   | 1234 | Engineer | 2
Harry Shearstone | 1234 | Engineer | 3
Tom Barker       | 1234 | Engineer | 4
Lewis Lockwood   | 1234 | Engineer | 5
Lance Duncan     | 1234 | Engineer | 6
Pete King        | 1234 | Engineer | 7
Graham Denman    | 1234 | Engineer | 8
Keith Wilton     | 1234 | Engineer | 9
Rob Appleyard    | 1234 | Engineer | 10
Mike Adams       | 1234 | Engineer | 11
Mick Thornley    | 1234 | Engineer | 12
David Williams   | 1234 | Engineer | 13
Kevin Deakin     | 1234 | Engineer | 14
Management       | 1234 | Manager  | ALL
```

**IMPORTANT**: Each engineer should change their PIN after first login!

---

## STEP 3: Setup StockMaster Sheet

In the **StockMaster** sheet, add these columns:
```
PartNumber | PartDescription | StandardMin | StandardMax | UnitPrice | Category
```

Import the data from `stock_master_import.csv` (provided separately).

This contains all 59 parts from the Michael Nicoletti van stock list with suggested min/max values.

---

## STEP 4: Setup VanInventory Sheet

In the **VanInventory** sheet, add these columns:
```
VanNumber | PartNumber | Quantity | PartDescription | MinQuantity | MaxQuantity | UnitPrice | TotalValue | LastModified | EngineerName
```

### Initial Stock Population Script

You can populate all 15 vans with the same stock list using this Apps Script function:

```javascript
function populateAllVans() {
  const ss = SpreadsheetApp.getActiveSpreadsheet();
  const masterSheet = ss.getSheetByName('StockMaster');
  const inventorySheet = ss.getSheetByName('VanInventory');
  const usersSheet = ss.getSheetByName('Users');
  
  // Get all engineers (skip header, skip Management)
  const users = usersSheet.getDataRange().getValues();
  const engineers = users.slice(1).filter(user => user[2] === 'Engineer');
  
  // Get all parts from master
  const masterData = masterSheet.getDataRange().getValues();
  const parts = masterData.slice(1); // Skip header
  
  // Clear existing inventory (except header)
  if (inventorySheet.getLastRow() > 1) {
    inventorySheet.getRange(2, 1, inventorySheet.getLastRow() - 1, 10).clear();
  }
  
  // Populate each van
  engineers.forEach(engineer => {
    const vanNumber = engineer[3]; // VanNumber column
    const engineerName = engineer[0]; // Engineer name column
    
    parts.forEach(part => {
      const row = [
        vanNumber,                    // VanNumber
        part[0],                      // PartNumber
        part[3] || 0,                 // Quantity (start with StandardMin or 0)
        part[1],                      // PartDescription
        part[2],                      // MinQuantity
        part[3],                      // MaxQuantity
        part[4],                      // UnitPrice
        `=(C${inventorySheet.getLastRow() + 1}*G${inventorySheet.getLastRow() + 1})`, // TotalValue formula
        new Date(),                   // LastModified
        engineerName                  // EngineerName
      ];
      
      inventorySheet.appendRow(row);
    });
  });
  
  Logger.log('All vans populated successfully!');
  SpreadsheetApp.getUi().alert('All vans populated with stock from master list!');
}
```

Run this function once to populate all 15 vans with the initial stock.

---

## STEP 5: Deploy Google Apps Script

1. In your Google Sheet, go to **Extensions > Apps Script**
2. Delete any default code
3. Paste the contents of `Code.gs` (provided)
4. Update the `SPREADSHEET_ID` at the top:
   - Get your Sheet ID from the URL: `https://docs.google.com/spreadsheets/d/[THIS_IS_YOUR_ID]/edit`
5. Click **Deploy > New deployment**
6. Choose **Web app**
7. Settings:
   - Description: "Van Stock Management API"
   - Execute as: **Me**
   - Who has access: **Anyone**
8. Click **Deploy**
9. Copy the **Web app URL** - you'll need this for the frontend

---

## STEP 6: Setup Frontend

### Option A: GitHub Pages (Recommended)

1. Create new GitHub repository: `van-stock-management`
2. Upload `index.html` to the repository
3. In `index.html`, update line ~600:
   ```javascript
   const API_URL = 'YOUR_GOOGLE_APPS_SCRIPT_URL_HERE';
   ```
   Replace with the Web app URL from Step 5

4. Enable GitHub Pages:
   - Settings > Pages
   - Source: main branch
   - Save

5. Your app URL will be: `https://yourusername.github.io/van-stock-management/`

### Option B: Duda Website

1. Update `index.html` with your Apps Script URL (line ~600)
2. Try embedding in Duda using Custom HTML widget
3. If Duda blocks it, use GitHub Pages and embed as iframe:
   ```html
   <iframe src="https://yourusername.github.io/van-stock-management/" 
           width="100%" 
           height="800px" 
           style="border:none;">
   </iframe>
   ```

---

## STEP 7: Testing

### Test Login
1. Open the app
2. Select "Management"
3. Enter PIN: 1234
4. Should see dashboard with all vans

### Test Engineer View
1. Logout
2. Select "Aaron Dyson"
3. Enter PIN: 1234
4. Should see Van 1 stock only
5. Try updating a quantity
6. Verify it saves to Google Sheets

### Test Features
- ✅ Dashboard shows all vans
- ✅ Search/filter works
- ✅ Quantity updates save
- ✅ Replenishment list shows items below min
- ✅ Audit export downloads CSV

---

## Security Notes

1. **Change PINs**: All engineers should change default PIN (1234)
2. **Sheet Protection**: Protect Users sheet so only you can edit it
3. **API URL**: Keep your Apps Script URL private
4. **Backup**: Regularly export Sheet to Excel as backup

---

## Customization

### Add New Parts
1. Add to **StockMaster** sheet
2. Run `populateAllVans()` again (or manually add to specific vans)

### Change Min/Max Values
Update directly in **VanInventory** sheet for specific vans, or **StockMaster** for defaults

### Add More Vans
1. Add engineer to **Users** sheet with new van number
2. Add their stock to **VanInventory** sheet

---

## Maintenance

### Weekly Tasks
- Review replenishment lists
- Check stock audit values
- Verify engineers are updating stock

### Monthly Tasks
- Backup Google Sheet to Excel
- Review and adjust min/max values
- Check for obsolete parts

---

## Troubleshooting

### "Connection error" on login
- Check API_URL is correct in index.html
- Verify Apps Script deployment is "Anyone can access"
- Check browser console for CORS errors

### Stock not updating
- Verify engineer has correct van number in Users sheet
- Check LastModified column updates
- Test with Management account

### Missing data
- Verify all sheet names are exact: Users, VanInventory, StockMaster
- Check SPREADSHEET_ID in Apps Script
- Run setupSheets() function in Apps Script

---

## Support

For issues:
1. Check browser console (F12) for errors
2. Check Apps Script logs (Execution log)
3. Verify Google Sheets data structure
4. Test with Management account first

---

## Files Included

1. `Code.gs` - Google Apps Script backend
2. `index.html` - Frontend application
3. `stock_master_import.csv` - Initial stock data (59 parts)
4. `SETUP.md` - This guide
5. `README.md` - User guide

---

## Next Steps

1. ✅ Create Google Sheet with 3 sheets
2. ✅ Add users to Users sheet
3. ✅ Import stock data to StockMaster
4. ✅ Run populateAllVans() to populate all vans
5. ✅ Deploy Apps Script as web app
6. ✅ Update API_URL in index.html
7. ✅ Deploy to GitHub Pages or Duda
8. ✅ Test with Management login
9. ✅ Test with Engineer login
10. ✅ Change all default PINs!

---

## Database Schema Reference

### Users Table
- Engineer (TEXT) - Name of engineer
- PIN (TEXT) - 4-digit PIN code
- Role (TEXT) - "Engineer" or "Manager"
- VanNumber (NUMBER/TEXT) - Van number (1-15) or "ALL" for management

### VanInventory Table
- VanNumber (NUMBER) - Van number (1-15)
- PartNumber (TEXT) - Unique part identifier
- Quantity (NUMBER) - Current stock level
- PartDescription (TEXT) - Part description
- MinQuantity (NUMBER) - Minimum stock level
- MaxQuantity (NUMBER) - Maximum stock level
- UnitPrice (NUMBER) - Price per unit (£)
- TotalValue (FORMULA) - =Quantity * UnitPrice
- LastModified (DATE) - Last update timestamp
- EngineerName (TEXT) - Engineer responsible

### StockMaster Table
- PartNumber (TEXT) - Unique part identifier
- PartDescription (TEXT) - Part description
- StandardMin (NUMBER) - Default minimum quantity
- StandardMax (NUMBER) - Default maximum quantity
- UnitPrice (NUMBER) - Current unit price (£)
- Category (TEXT) - Part category/group
