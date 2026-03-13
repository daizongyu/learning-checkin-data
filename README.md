# Learning Check-in Data Repository

Global learning check-in data storage for OpenClaw users.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Update](https://img.shields.io/badge/update-daily-blue.svg)](https://github.com/daizongyu/learning-checkin-data/actions)

---

## Overview

This is a **public data repository** that stores learning check-in records from users worldwide. It serves as the centralized data backend for the [Learning Check-in Skill](https://github.com/daizongyu/learning-checkin).

### Purpose

- Store user profiles and check-in records
- Track consecutive learning streaks
- Maintain global and country-specific leaderboards
- Enable anonymous participation (no GitHub account required)

---

## Data Structure

```
.
├── users/                      # User data directory
│   └── {user_id}/             # Individual user directory
│       ├── profile.json       # User profile
│       ├── streak.json        # Streak statistics
│       └── checkins/          # Daily check-in records
│           └── YYYY-MM-DD.json
├── leaderboard/               # Leaderboard data
│   └── current.json           # Current rankings
└── skill/                     # Skill metadata
    └── version.json           # Version information
```

---

## File Formats

### User Profile (`users/{user_id}/profile.json`)

```json
{
  "user_id": "openclaw_daisy_a1b2c3",
  "nickname": "Daisy",
  "country": "CN",
  "created_at": "2025-01-20T10:00:00Z",
  "status": "active",
  "reminder_time": "20:00",
  "reminder_style": "warm"
}
```

### Streak Statistics (`users/{user_id}/streak.json`)

```json
{
  "user_id": "openclaw_daisy_a1b2c3",
  "current_streak": 15,
  "total_checkins": 42,
  "longest_streak": 21,
  "last_checkin_date": "2025-01-20",
  "failed_weeks": 0
}
```

### Daily Check-in (`users/{user_id}/checkins/YYYY-MM-DD.json`)

```json
{
  "user_id": "openclaw_daisy_a1b2c3",
  "date": "2025-01-20",
  "checked": true,
  "timestamp": "2025-01-20T12:30:00Z",
  "note": "Studied Python for 2 hours"
}
```

### Leaderboard (`leaderboard/current.json`)

```json
{
  "last_updated": "2025-01-20T00:00:00Z",
  "update_method": "automated",
  "total_users": 150,
  "rankings": [
    {
      "rank": 1,
      "user_id": "openclaw_alice_x9y8z7",
      "nickname": "Alice",
      "country": "US",
      "current_streak": 120,
      "total_checkins": 150,
      "longest_streak": 120
    }
  ]
}
```

---

## Automated Updates

### Leaderboard

The leaderboard is automatically updated **daily at UTC 00:00** (Beijing Time 08:00) via GitHub Actions.

- **Workflow**: `.github/workflows/update_leaderboard.yml`
- **Script**: `.github/workflows/update_leaderboard.py`
- **Trigger**: Scheduled cron job + manual dispatch

### Update Process

1. Scan all user directories
2. Collect streak statistics
3. Calculate rankings (sorted by current streak)
4. Update `leaderboard/current.json`
5. Commit and push changes

---

## Privacy

### What We Store

- ✅ User ID (anonymous, auto-generated)
- ✅ Nickname (user-provided, can be pseudonym)
- ✅ Country code (e.g., CN, US, UK)
- ✅ Check-in dates and streaks
- ✅ Optional check-in notes

### What We DON'T Store

- ❌ Real names
- ❌ Email addresses
- ❌ GitHub usernames
- ❌ IP addresses
- ❌ Any personal sensitive information

### Anonymity

- User IDs follow the format: `openclaw_{nickname}_{random}`
- No authentication required to participate
- All data is public (this is a public repository)
- Users can use pseudonyms for privacy

---

## Rules

### Check-in Rules

1. **Daily Check-in**: At least one check-in per day
2. **Streak Tracking**: Consecutive days are counted automatically
3. **Failure Rule**: Task fails if ≥2 days missed per week
4. **Restart**: Can rejoin anytime after failure

### Data Integrity

- Do not manually edit other users' data
- Do not delete or modify leaderboard files
- Do not commit spam or test data
- Respect the repository structure

---

## For Developers

### API Access

All data is stored in JSON format and accessible via GitHub API:

```bash
# Get user profile
curl https://api.github.com/repos/daizongyu/learning-checkin-data/contents/users/openclaw_daisy_a1b2c3/profile.json

# Get leaderboard
curl https://api.github.com/repos/daizongyu/learning-checkin-data/contents/leaderboard/current.json
```

### Rate Limits

- **Unauthenticated**: 60 requests/hour
- **Authenticated**: 5000 requests/hour (recommended)

### GitHub Actions

The repository uses GitHub Actions for automated tasks:

| Workflow | Frequency | Purpose |
|----------|-----------|---------|
| `update_leaderboard.yml` | Daily (UTC 00:00) | Update rankings |

---

## Related Projects

- **[Learning Check-in Skill](https://github.com/daizongyu/learning-checkin)**: Main code repository
- **[OpenClaw](https://github.com/OpenClaw-Skills)**: Parent project

---

## Contributing

This is a data repository managed by the Learning Check-in Skill. Users interact with it through the Skill CLI, not directly.

To contribute to the project:

1. Visit the [code repository](https://github.com/daizongyu/learning-checkin)
2. Fork and create a feature branch
3. Make your changes
4. Submit a pull request

---

## Support

- **Documentation**: https://github.com/daizongyu/learning-checkin/blob/main/SKILL.md
- **Quick Start**: https://github.com/daizongyu/learning-checkin/blob/main/QUICKSTART.md
- **Issues**: https://github.com/daizongyu/learning-checkin/issues

---

## License

MIT License - See [LICENSE](LICENSE) file for details.

---

**Learn together, grow together!** 🦐📚✨
