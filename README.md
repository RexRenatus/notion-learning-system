# 📚 Notion Learning System

> Transform scattered educational tracking into a unified, gamified Notion workspace with AI-powered insights

[![Project Status](https://img.shields.io/badge/status-phase%203-yellow)](https://github.com/RexRenatus/notion-learning-system)
[![Documentation](https://img.shields.io/badge/docs-comprehensive-green)](./planning/PROJECT_INDEX.md)
[![License](https://img.shields.io/badge/license-MIT-blue)](./LICENSE)

## 🎯 Overview

The Notion Learning System is a comprehensive educational tracking framework that transforms how you manage and gamify your learning journey. Built entirely in Notion, it features 10 interconnected databases, progress tracking, XP systems, and AI-powered insights.

### Key Features

- 🎮 **Gamification**: XP system, levels, achievements, and streaks
- 📊 **Progress Tracking**: Automated formulas calculate progress across all goals
- 🤖 **AI Integration**: Daily summaries, insights, and goal decomposition
- 📱 **Multi-Platform**: Works on all devices through Notion
- 🔄 **Automation**: Smart formulas and rollups reduce manual work
- 📈 **Analytics**: Dashboard views for daily, weekly, and monthly insights

## 🚀 Quick Start

### Prerequisites

- Notion account (Free or Paid)
- Basic familiarity with Notion databases
- 30-60 minutes for initial setup

### Installation

1. **Clone this repository**
   ```bash
   git clone git@github.com:RexRenatus/notion-learning-system.git
   cd notion-learning-system
   ```

2. **Follow Phase 2 Implementation**
   ```bash
   # Start with Subject Master database
   cat Phase2_Foundation/databases/SUBJECT_MASTER_STEPS.md
   ```

3. **Create databases in order**:
   - Subject Master
   - Goals Hierarchy
   - Daily Actions
   - Daily Learning Sessions
   - Journal Entries

4. **Add Phase 3 formulas**:
   ```bash
   # View all formulas
   cat Phase3_Automation/formulas/CORRECTED_FORMULAS_GUIDE.md
   ```

## 📂 Project Structure

```
notion-learning-system/
├── Phase1_Pseudocode/       # Design documents & requirements
│   ├── analysis/            # Requirements analysis
│   ├── design/              # System architecture
│   └── schemas/             # Database schemas
├── Phase2_Foundation/       # Database setup guides
│   ├── databases/           # Step-by-step guides
│   └── testing/             # Testing procedures
├── Phase3_Automation/       # Formulas & automation
│   ├── formulas/            # Progress calculations
│   └── xp_system/           # Gamification logic
├── planning/                # Project management
│   ├── MASTER_TODO.md       # Task tracking
│   ├── PROJECT_JOURNAL.md   # Development log
│   └── PHASE_ROADMAP.md     # Implementation phases
└── CLAUDE.md               # AI assistant guidelines
```

## 🗄️ Database Overview

### Core Databases

1. **📚 Subject Master** - Track all learning subjects
   - Levels, XP, streaks
   - Study goals and resources
   - Progress monitoring

2. **🎯 Goals Hierarchy** - Hierarchical goal management
   - Yearly → Quarterly → Monthly → Weekly → Daily
   - Progress tracking with formulas
   - Automated status updates

3. **✅ Daily Actions** - Task management
   - Linked to goals and subjects
   - Priority scoring
   - XP rewards

4. **📖 Daily Learning Sessions** - Study tracking
   - Duration and quality metrics
   - XP calculation
   - Session insights

5. **📓 Journal Entries** - Daily reflection
   - Full-page journaling
   - AI analysis integration
   - Productivity metrics

### Supporting Databases (Phase 4+)

6. **🔄 Process Library** - Reusable workflows
7. **🏆 Achievements** - Unlockable rewards
8. **📊 Progress Snapshots** - Historical tracking
9. **💰 Learning Investments** - Financial tracking
10. **🔔 Notification Queue** - Reminder system

## 📊 Current Status

### ✅ Phase 1: Design & Analysis (Complete)
- System architecture designed
- All 10 databases specified
- Requirements documented
- AI integration planned

### ✅ Phase 2: Foundation (Complete)
- Core 5 databases implemented
- Relations established
- Basic properties configured
- Testing procedures created

### 🚧 Phase 3: Automation (In Progress)
- ✅ Progress formulas implemented
- ✅ XP system designed
- ⏳ Dashboard views pending
- ⏳ Weekly analytics pending

### 📅 Upcoming Phases
- **Phase 4**: Advanced gamification
- **Phase 5**: External integrations
- **Phase 6**: AI automation

## 🎮 XP & Gamification

### XP Sources
- **Learning Sessions**: 1 XP per minute (with multipliers)
- **Daily Actions**: 20-50 XP based on type
- **Goal Completion**: 50-5000 XP by goal level
- **Achievements**: Special rewards

### Level System
- Levels 1-100+ with titles
- XP requirements: Level² × 100
- Visual progress tracking
- Leaderboards

### Multipliers
- 🎯 Deep Focus: 1.5x
- 🔥 Streak Bonus: Up to 2.0x
- ⏰ Early Completion: 1.5x

## 🛠️ Configuration

### Formula Customization

Edit formulas in your Notion databases:

1. **Progress Calculation** - Adjust thresholds
2. **XP Multipliers** - Modify reward rates
3. **Status Indicators** - Change visual cues

### View Templates

Pre-configured views:
- Today's Dashboard
- Weekly Analytics
- Subject Overview
- Achievement Gallery

## 🤝 Contributing

We welcome contributions! Please:

1. Fork the repository
2. Create a feature branch
3. Follow existing documentation style
4. Update relevant guides
5. Submit a pull request

### Development Guidelines

- Update `MASTER_TODO.md` after completing tasks
- Add entries to `PROJECT_JOURNAL.md`
- Follow rules in `CLAUDE.md`
- Test all formulas before committing

## 📚 Documentation

- **[Project Index](./PROJECT_INDEX.md)** - Complete file listing
- **[Phase Roadmap](./planning/PHASE_ROADMAP.md)** - Implementation plan
- **[Architecture Decisions](./planning/ARCHITECTURE_DECISIONS.md)** - Design choices
- **[Formula Guide](./Phase3_Automation/formulas/CORRECTED_FORMULAS_GUIDE.md)** - All formulas

## ⚠️ Known Limitations

### Notion Constraints
- Cannot access related item properties in formulas
- No dynamic date filtering in rollups
- Limited automation without API

### Workarounds
- Use rollups instead of formula references
- Create filtered views for time-based data
- Manual weekly resets for some metrics

## 🐛 Troubleshooting

### Common Issues

1. **"Property not found" in formulas**
   - Use dropdown to select properties
   - Check exact property names (case-sensitive)

2. **XP not calculating**
   - Ensure all rollups are set up first
   - Check relation connections

3. **Progress showing 0%**
   - Verify Actions are linked to Goals
   - Check completion status checkboxes

### Getting Help

- Check [Troubleshooting Guide](./Phase2_Foundation/databases/TROUBLESHOOTING_ROLLUPS.md)
- Review [Formula Limitations](./Phase3_Automation/NOTION_FORMULA_LIMITATIONS.md)
- Open an issue on GitHub

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](./LICENSE) file for details.

## 🙏 Acknowledgments

- Notion team for the amazing platform
- Claude AI for development assistance
- Community contributors

## 📮 Contact

- **GitHub**: [RexRenatus/notion-learning-system](https://github.com/RexRenatus/notion-learning-system)
- **Issues**: [Report bugs or request features](https://github.com/RexRenatus/notion-learning-system/issues)

---

<p align="center">
  Built with ❤️ for lifelong learners<br>
  <em>Transform your learning journey today!</em>
</p>