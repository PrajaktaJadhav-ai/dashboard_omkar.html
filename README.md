<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Admin Dashboard - Omkar Ekale | Real Estate Pune</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800&display=swap" rel="stylesheet">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Poppins', sans-serif; background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); min-height: 100vh; }
        
        /* Sidebar */
        .sidebar {
            position: fixed;
            left: 0;
            top: 0;
            width: 280px;
            height: 100vh;
            background: linear-gradient(180deg, #1e3c72 0%, #2a5298 100%);
            color: white;
            padding: 2rem 0;
            z-index: 1000;
            box-shadow: 4px 0 20px rgba(0,0,0,0.1);
        }
        .logo {
            text-align: center;
            font-size: 2rem;
            font-weight: 800;
            background: linear-gradient(135deg, #ff8c42, #ffb366);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 3rem;
            padding: 0 2rem;
        }
        .nav-menu {
            list-style: none;
            padding: 0 1.5rem;
        }
        .nav-item {
            margin-bottom: 1rem;
        }
        .nav-link {
            display: flex;
            align-items: center;
            gap: 1rem;
            color: rgba(255,255,255,0.9);
            text-decoration: none;
            padding: 1rem 1.5rem;
            border-radius: 15px;
            transition: all 0.3s;
            font-weight: 500;
        }
        .nav-link:hover, .nav-link.active {
            background: rgba(255,255,255,0.15);
            color: white;
            transform: translateX(10px);
        }
        .nav-link i { font-size: 1.2rem; width: 20px; }
        
        /* Main Content */
        .main-content {
            margin-left: 280px;
            padding: 2rem;
            min-height: 100vh;
        }
        .header {
            background: white;
            padding: 2rem;
            border-radius: 20px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.1);
            margin-bottom: 2rem;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .welcome-text h1 {
            font-size: 2.5rem;
            color: #1e3c72;
            margin-bottom: 0.5rem;
        }
        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 2rem;
            margin: 2rem 0;
        }
        .stat-card {
            background: white;
            padding: 2rem;
            border-radius: 20px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.08);
            text-align: center;
            transition: all 0.3s;
            border-top: 4px solid transparent;
        }
        .stat-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 60px rgba(0,0,0,0.15);
        }
        .stat-card.leads { border-top-color: #25D366; }
        .stat-card.properties { border-top-color: #ff8c42; }
        .stat-card.revenue { border-top-color: #28a745; }
        .stat-number {
            font-size: 3rem;
            font-weight: 800;
            color: #1e3c72;
            margin-bottom: 0.5rem;
        }
        .stat-label { font-size: 1.1rem; color: #666; font-weight: 500; }
        
        /* Leads Table */
        .section-card {
            background: white;
            padding: 2rem;
            border-radius: 20px;
            box-shadow: 0 10px 40px rgba(0,0,0,0.08);
            margin-bottom: 2rem;
        }
        .section-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 2rem;
        }
        .section-title {
            font-size: 1.8rem;
            color: #1e3c72;
            font-weight: 700;
        }
        .table-container {
            overflow-x: auto;
            border-radius: 15px;
            box-shadow: 0 5px 20px rgba(0,0,0,0.08);
        }
        table {
            width: 100%;
            border-collapse: collapse;
            background: white;
        }
        th, td {
            padding: 1.2rem 1rem;
            text-align: left;
            border-bottom: 1px solid #eee;
        }
        th {
            background: linear-gradient(135deg, #ff8c42, #f7931e);
            color: white;
            font-weight: 600;
            position: sticky;
            top: 0;
        }
        tr:hover {
            background: #f8f9fa;
        }
        .status {
            padding: 0.4rem 1rem;
            border-radius: 20px;
            font-size: 0.85rem;
            font-weight: 600;
        }
        .status.new { background: #fff3cd; color: #856404; }
        .status.contacted { background: #d1ecf1; color: #0c5460; }
        .status.closed { background: #d4edda; color: #155724; }
        .action-btn {
            padding: 0.5rem 1rem;
            border: none;
            border-radius: 20px;
            cursor: pointer;
            font-weight: 600;
            text-decoration: none;
            display: inline-block;
            margin-right: 0.5rem;
            transition: all 0.3s;
        }
        .btn-whatsapp { background: #25D366; color: white; }
        .btn-call { background: #007bff; color: white; }
        .btn-call:hover { background: #0056b3; }
        .btn-whatsapp:hover { background: #20c95b; }
        
        /* Properties Form */
        .form-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 2rem;
        }
        .form-group {
            margin-bottom: 1.5rem;
        }
        .form-group label {
            display: block;
            margin-bottom: 0.5rem;
            font-weight: 600;
            color: #1e3c72;
        }
        .form-group input, .form-group select, .form-group textarea {
            width: 100%;
            padding: 1rem;
            border: 2px solid #e0e0e0;
            border-radius: 12px;
            font-size: 1rem;
            transition: border-color 0.3s;
        }
        .form-group input:focus, .form-group select:focus, .form-group textarea:focus {
            outline: none;
            border-color: #ff8c42;
        }
        .btn-primary {
            background: linear-gradient(135deg, #ff8c42, #f7931e);
            color: white;
            padding: 1rem 2rem;
            border: none;
            border-radius: 25px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
        }
        .btn-primary:hover {
            transform: translateY(-2px);
            box-shadow: 0 10px 30px rgba(255,140,66,0.4);
        }
        
        /* Responsive */
        @media (max-width: 768px) {
            .sidebar { width: 100%; height: auto; position: relative; }
            .main-content { margin-left: 0; }
            .header { flex-direction: column; text-align: center; gap: 1rem; }
        }
        
        /* Animations */
        @keyframes fadeInUp {
            from { opacity: 0; transform: translateY(30px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .fade-in { animation: fadeInUp 0.8s ease-out; }
    </style>
</head>
<body>
    <!-- Sidebar -->
    <div class="sidebar">
        <div class="logo">
            <i class="fas fa-home"></i> Omkar Ekale
        </div>
        <ul class="nav-menu">
            <li class="nav-item"><a href="#dashboard" class="nav-link active"><i class="fas fa-chart-dashboard"></i> Dashboard</a></li>
            <li class="nav-item"><a href="#leads" class="nav-link"><i class="fas fa-users"></i> Leads</a></li>
            <li class="nav-item"><a href="#properties" class="nav-link"><i class="fas fa-building"></i> Properties</a></li>
            <li class="nav-item"><a href="#analytics" class="nav-link"><i class="fas fa-chart-line"></i> Analytics</a></li>
            <li class="nav-item"><a href="#website" class="nav-link"><i class="fas fa-globe"></i> Website</a></li>
            <li class="nav-item"><a href="../index.html" class="nav-link"><i class="fas fa-arrow-left"></i> Live Site</a></li>
        </ul>
    </div>

    <!-- Main Content -->
    <div class="main-content">
        <!-- Header -->
        <div class="header fade-in">
            <div class="welcome-text">
                <h1>Admin Dashboard</h1>
                <p>Welcome back, Omkar! Here's what's happening with your real estate business.</p>
            </div>
            <div style="display: flex; gap: 1rem;">
                <button class="btn-primary" onclick="exportLeads()">
                    <i class="fas fa-download"></i> Export CSV
                </button>
                <button class="btn-primary" onclick="refreshData()">
                    <i class="fas fa-sync-alt"></i> Refresh
                </button>
            </div>
        </div>

        <!-- Stats Cards -->
        <div class="stats-grid">
            <div class="stat-card leads fade-in">
                <div class="stat-number" id="totalLeads">127</div>
                <div class="stat-label">Total Leads</div>
            </div>
            <div class="stat-card properties fade-in">
                <div class="stat-number" id="totalProperties">23</div>
                <div class="stat-label">Active Properties</div>
            </div>
            <div class="stat-card revenue fade-in">
                <div class="stat-number" id="conversionRate">18%</div>
                <div class="stat-label">Conversion Rate</div>
            </div>
        </div>

        <!-- Leads Section -->
        <div class="section-card fade-in" id="leadsSection">
            <div class="section-header">
                <h2 class="section-title">📞 New Leads</h2>
                <span style="color: #25D366; font-weight: 600;">Live from Google Sheets</span>
            </div>
            <div class="table-container">
                <table id="leadsTable">
                    <thead>
                        <tr>
                            <th>Name</th>
                            <th>Phone</th>
                            <th>Property Type</th>
                            <th>Budget</th>
                            <th>Message</th>
                            <th>Date</th>
                            <th>Status</th>
                            <th>Actions</th>
                        </tr>
                    </thead>
                    <tbody id="leadsTableBody">
                        <!-- Leads populated by JavaScript -->
                    </tbody>
                </table>
            </div>
        </div>

        <!-- Add Property Section -->
        <div class="section-card fade-in" id="propertiesSection" style="display: none;">
            <div class="section-header">
                <h2 class="section-title">🏠 Add New Property</h2>
            </div>
            <form id="propertyForm" class="form-grid">
                <div class="form-group">
                    <label>Property Title</label>
                    <input type="text" name="title" placeholder="3BHK Luxury Apartment" required>
                </div>
                <div class="form-group">
                    <label>Price</label>
                    <input type="text" name="price" placeholder="₹90 Lac" required>
                </div>
                <div class="form-group">
                    <label>Category</label>
                    <select name="category" required>
                        <option value="residential">Residential</option>
                        <option value="commercial">Commercial</option>
                        <option value="investment">Investment</option>
                    </select>
                </div>
                <div class="form-group">
                    <label>Location</label>
                    <input type="text" name="location" placeholder="Hinjewadi Phase 1" required>
                </div>
                <div class="form-group">
                    <label>Details</label>
                    <textarea name="details" rows="4" placeholder="1250 sqft, 3BHK, Ready to move"></textarea>
                </div>
                <button type="submit" class="btn-primary">Add Property</button>
            </form>
        </div>
    </div>

    <script>
        // Mock data - Replace with your Google Sheets API
        const mockLeads = [
            {name: "Rahul Sharma", phone: "9876543210", property: "Residential 2BHK", budget: "₹60L", message: "Hinjewadi area", date: "2024-01-15", status: "new"},
            {name: "Priya Patel", phone: "9123456789", property: "Commercial", budget: "₹2Cr", message: "Office space Baner", date: "2024-01-14", status: "contacted"},
            {name: "Amit Singh", phone: "9988776655", property: "Investment", budget: "₹1Cr", message: "High ROI plots", date: "2024-01-13", status: "closed"}
        ];

        // Navigation
        document.querySelectorAll('.nav-link').forEach(link => {
            link.addEventListener('click', function(e) {
                e.preventDefault();
                document.querySelectorAll('.nav-link').forEach(l => l.classList.remove('active'));
                this.classList.add('active');
                
                const target = this.getAttribute('href').substring(1);
                showSection(target);
            });
        });

        function showSection(section) {
            // Hide all sections
            document.querySelectorAll('.section-card').forEach(card => {
                card.style.display = 'none';
            });
            
            if(section === 'leads') {
                document.getElementById('leadsSection').style.display = 'block';
                loadLeads();
            } else if(section === 'properties') {
                document.getElementById('propertiesSection').style.display = 'block';
            }
        }

        // Load leads from Google Sheets (mock data for now)
        function loadLeads() {
            const tbody = document.getElementById('leadsTableBody');
            tbody.innerHTML = '';
            
            mockLeads.forEach(lead => {
                const row = `
                    <tr>
                        <td><strong>${lead.name}</strong></td>
                        <td><a href="tel:${lead.phone}" class="btn-call" style="font-size: 0.9rem; padding: 0.4rem 0.8rem;">${lead.phone}</a></td>
                        <td>${lead.property}</td>
                        <td>${lead.budget}</td>
                        <td>${lead.message}</td>
                        <td>${lead.date}</td>
                        <td><span class="status ${lead.status}">${lead.status.toUpperCase()}</span></td>
                        <td>
                            <a href="https://wa.me/${lead.phone}?text=Hi ${lead.name}, regarding your property enquiry..." 
                               class="action-btn btn-whatsapp" target="_blank">
                                <i class="fab fa-whatsapp"></i> WhatsApp
                            </a>
                            <a href="tel:${lead.phone}" class="action-btn btn-call">
                                <i class="fas fa-phone"></i> Call
                            </a>
                        </td>
                    </tr>
                `;
                tbody.innerHTML += row;
            });
        }

        // Property form
        document.getElementById('propertyForm').addEventListener('submit', function(e) {
            e.preventDefault();
            alert('✅ Property added successfully! Update your website HTML with new property card.');
            this.reset();
        });

        // Export leads
        function exportLeads() {
            const csv = 'Name,Phone,Property,Budget,Message,Date,Status\n' + 
                       mockLeads.map(l => `${l.name},${l.phone},${l.property},${l.budget},${l.message},${l.date},${l.status}`).join('\n');
            const blob = new Blob([csv], { type: 'text/csv' });
            const url = window.URL.createObjectURL(blob);
            const a = document.createElement('a');
            a.href = url;
            a.download = 'omkar-leads.csv';
            a.click();
        }

        // Refresh data
        function refreshData() {
            alert('🔄 Data refreshed from Google Sheets!');
            loadLeads();
        }

        // Initialize
        document.addEventListener('DOMContentLoaded', function() {
            loadLeads();
        });
    </script>
</body>
</html>
