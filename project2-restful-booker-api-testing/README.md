# Restful-Booker API Testing

Professional API testing suite for a hotel booking system.

## 🚀 What I Built
- **End-to-end testing** of booking lifecycle (create → read → update → delete)
- **Authentication workflow** with token management
- **7 API endpoints** tested with Postman
- **Automated test suite**

## 🛠️ Technical Implementation
- **Postman Collection** with JavaScript tests
- **Cookie-based authentication**
- **Dynamic variable passing** between requests
- **Status code & data validation** assertions

## 📊 Test Coverage
| Endpoint | Method | Auth | Tests |
|----------|--------|------|-------|
| `/auth` | POST | No | Token generation & validation |
| `/booking` | GET | No | List all bookings |
| `/booking` | POST | No | Create new booking |
| `/booking/:id` | GET | No | Get specific booking |
| `/booking/:id` | PUT | Yes | Full update |
| `/booking/:id` | PATCH | Yes | Partial update |
| `/booking/:id` | DELETE | Yes | Delete booking |

## 🎯 Key Challenges Solved
1. **Token Management**: Implemented secure variable passing
2. **Test Sequencing**: Built dependent workflow in Collection Runner

## 📁 Files
- `postman-collection.json` - Import into Postman to run tests
- `evidence/` - Collection structure and test results

## 🚀 Quick Start
1. Import `postman-collection.json` into Postman
2. Run the "Happy Path" collection
3. All tests should pass (15+ assertions)

## 💡 Skills Demonstrated
- API Testing, Postman, JavaScript, Test Automation, Troubleshooting
