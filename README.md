# 🚐 Van Stock Management System

> Real-time stock tracking and management for 15 service vans at Narrow Aisle Ltd

## Features

### For Engineers
- ✅ View your van's current stock levels
- ✅ Update quantities using tablet-friendly interface
- ✅ See replenishment needs instantly
- ✅ Min/Max stock level alerts
- ✅ Secure PIN login

### For Management
- ✅ Dashboard view of entire fleet
- ✅ Real-time stock levels across all vans
- ✅ Generate replenishment pick lists
- ✅ Export stock audits to Excel
- ✅ Monitor stock values
- ✅ Search across entire fleet

## Technology Stack

- **Backend**: Google Apps Script (serverless)
- **Database**: Google Sheets
- **Frontend**: HTML, CSS, JavaScript (vanilla)
- **Hosting**: GitHub Pages or Duda embed
- **No dependencies**: Works offline once loaded

## Quick Start

### 1. Setup Google Sheet (5 minutes)

```
1. Create new Google Sheet: "Van Stock Management"
2. Create 3 tabs: Users, VanInventory, StockMaster
3. Follow SETUP.md for detailed structure
```

### 2. Deploy Apps Script (3 minutes)

```
1. Extensions > Apps Script
2. Paste Code.gs content
3. Update SPREADSHEET_ID
4. Deploy as Web App (Anyone access)
5. Copy Web App URL
```

### 3. Deploy Frontend (2 minutes)

**Option A - GitHub Pages:**
```
1. Create GitHub repo
2. Upload index.html
3. Update API_URL with your Apps Script URL
4. Enable GitHub Pages
```

**Option B - Duda Website:**
```
1. Deploy to GitHub first
2. Embed as iframe in Duda:
   <iframe src="your-github-pages-url" width="100%" height="800px"></iframe>
```

## Architecture

```
┌─────────────────┐
│   Engineers     │
│   (Tablets)     │
└────────┬────────┘
         │
         ▼
┌─────────────────┐     ┌──────────────────┐
│   HTML/JS       │────▶│  Apps Script API │
│   Frontend      │◀────│  (Web App)       │
└─────────────────┘     └────────┬─────────┘
                                 │
                                 ▼
                        ┌─────────────────┐
                        │  Google Sheets  │
                        │                 │
                        │  • Users        │
                        │  • VanInventory │
                        │  • StockMaster  │
                        └─────────────────┘
```

## File Structure

```
van-stock-management/
│
├── index.html                  # Main frontend application
├── Code.gs                     # Google Apps Script backend
├── stock_master_import.csv     # Initial stock data (59 parts)
│
├── SETUP.md                    # Detailed setup instructions
├── USER_GUIDE.md               # User documentation
└── README.md                   # This file
```

## Database Schema

### Users
- Engineer, PIN, Role, VanNumber

### VanInventory
- VanNumber, PartNumber, Quantity, PartDescription
- MinQuantity, MaxQuantity, UnitPrice, TotalValue
- LastModified, EngineerName

### StockMaster
- PartNumber, PartDescription
- StandardMin, StandardMax, UnitPrice, Category

## Engineers List

1. Aaron Dyson - Van 1
2. Brett Stockton - Van 2
3. Harry Shearstone - Van 3
4. Tom Barker - Van 4
5. Lewis Lockwood - Van 5
6. Lance Duncan - Van 6
7. Pete King - Van 7
8. Graham Denman - Van 8
9. Keith Wilton - Van 9
10. Rob Appleyard - Van 10
11. Mike Adams - Van 11
12. Mick Thornley - Van 12
13. David Williams - Van 13
14. Kevin Deakin - Van 14
15. Management - All Vans

## Initial Stock

59 parts from Michael Nicoletti's van including:
- Contactors (Steer, Hydraulic, Regen, etc.)
- Bearings (Standard and HD)
- Fork Pin Kits
- Hoses and Gaskets
- Cables and Harnesses
- And more...

All parts include:
- Part numbers
- Descriptions
- Current pricing
- Suggested min/max levels based on usage

## Security

- ✅ PIN-based authentication
- ✅ Role-based access control (Engineer vs Manager)
- ✅ Engineers can only edit their own van
- ✅ Management has read access to all vans
- ✅ Audit trail with LastModified timestamps
- ✅ Google Sheets access control

**Default PIN**: 1234 (MUST be changed after first login!)

## Mobile/Tablet Friendly

- Responsive design works on all screen sizes
- Touch-optimized buttons and controls
- Easy +/- quantity adjustment
- Search functionality
- Works on iPads, Android tablets, phones

## Offline Support

- Frontend caches once loaded
- Works offline for viewing
- Syncs when connection restored
- No app store required

## Export Capabilities

### Replenishment Lists
- CSV format
- By van or fleet-wide
- Shows parts below minimum
- Includes quantities needed

### Stock Audits
- Full stock snapshot
- Current quantities and values
- Summary totals
- Timestamp included

## Maintenance

### Regular Tasks
- **Daily**: Engineers update after jobs
- **Weekly**: Review replenishment lists
- **Monthly**: Run stock audits
- **Quarterly**: Review and adjust min/max levels

### Backups
- Google Sheets auto-saves
- Download manual backups monthly
- Export to Excel for long-term storage

## Troubleshooting

### Connection Errors
1. Verify API_URL is correct
2. Check Apps Script deployment settings
3. Ensure "Anyone" can access web app

### Stock Not Updating
1. Check internet connection
2. Verify user has correct van number
3. Check Google Sheets permissions

### Missing Parts
1. Add to StockMaster sheet
2. Run populateAllVans() script
3. Or add manually to specific van

## Support

📧 **Setup Questions**: See SETUP.md
📖 **User Help**: See USER_GUIDE.md
🐛 **Issues**: Check browser console (F12)
💡 **Feature Requests**: Contact system admin

## Roadmap

### Phase 1 (Complete)
- ✅ Basic stock tracking
- ✅ PIN authentication
- ✅ Min/Max alerts
- ✅ Replenishment lists
- ✅ Stock audits

### Phase 2 (Future)
- 📱 Native mobile app
- 📊 Usage analytics
- 📧 Email alerts for low stock
- 🔔 Push notifications
- 📈 Trend analysis
- 🔄 Auto-replenishment

### Phase 3 (Future)
- 🚚 Supplier integration
- 📦 Purchase order generation
- 💰 Cost tracking
- 📊 Advanced reporting
- 🔍 Barcode scanning

## License

Internal use only - Narrow Aisle Ltd

## Credits

Built for Narrow Aisle Ltd van stock management
Engineers: 14 service engineers + management
Parts database: Based on Michael Nicoletti van stock list

---

**Version**: 1.0
**Last Updated**: December 2024
**Status**: Production Ready

## Getting Started Now

1. Read [SETUP.md](SETUP.md) for step-by-step installation
2. Read [USER_GUIDE.md](USER_GUIDE.md) for usage instructions
3. Import stock data from `stock_master_import.csv`
4. Deploy and test with management account
5. Train engineers
6. Go live! 🚀

---

For support or questions, contact your system administrator.
