# Contributing Guidelines

## Link Management Protocol ⚠️ CRITICAL

**Rule:** ALL files with external links MUST be verified before committing.

### When Adding/Updating Links

1. **Extract all links** from the file:
   ```bash
   grep -o 'https\?://[^)]\+' filename.md | sort -u
   ```

2. **Verify each link** manually or with a link checker

3. **Document in FULL-LINK-AUDIT.md**:
   - Add new links to appropriate section
   - Mark verification status (✅ verified, ⚠️ needs check, ❌ broken)
   - Note which files contain the link

4. **Update last audit date** in FULL-LINK-AUDIT.md

### Files That Contain Links

**Must be checked when modified:**
- `website/index.html` - Main curriculum (32 links)
- `week-*/README.md` - Week overviews
- `week-*/day-*.md` - Daily lesson files
- `projects/*/README.md` - Project documentation
- `build-in-public/*.md` - Social sharing templates

### Common Link Issues

**❌ Wrong patterns:**
- Old Anthropic docs: `docs.anthropic.com/en/docs/build-with-claude/agent-patterns`
- Typo in video IDs: `aqdWSYWC_LO` (should be `_LI`)
- Wrong video IDs: Using wrong creator's video

**✅ Correct patterns:**
- Anthropic blog: `www.anthropic.com/engineering/building-effective-agents`
- Anthropic tool docs: `docs.anthropic.com/en/docs/build-with-claude/tool-use/overview`
- YouTube video IDs: Always verify against video title/creator

### Verification Checklist

Before committing:
- [ ] Extracted all links from changed files
- [ ] Verified each link loads without 404
- [ ] Video IDs match video titles/creators
- [ ] Updated FULL-LINK-AUDIT.md
- [ ] Ran full audit if changing multiple files

### Link Audit Commands

**Extract all links from repo:**
```bash
find . -name "*.md" -o -name "*.html" | \
  xargs grep -oh 'https\?://[^)]\+' | \
  sort -u > /tmp/all-links.txt
```

**Find broken Anthropic links:**
```bash
grep -r "docs.anthropic.com.*agent-patterns" --include="*.md" --include="*.html" .
```

**Find duplicate video IDs:**
```bash
grep -oh 'watch?v=[^"&)]*' -r . | sort | uniq -d
```

## Content Updates

### Adding New Videos

1. Verify video exists and title matches
2. Check creator attribution is correct
3. Add to both:
   - Daily markdown file (week-X/day-Y.md)
   - Week README (week-X/README.md) if core resource
   - website/index.html if curriculum video
4. Update FULL-LINK-AUDIT.md

### Adding New Resources

1. Verify URL is permanent (not temporary/marketing link)
2. Check if resource is free/accessible
3. Add to appropriate section in FULL-LINK-AUDIT.md
4. Document source and purpose in markdown file

## Code Changes

### Screenshot Generator (scripts/screenshot.js)

- **DO NOT** commit node_modules
- Update package.json if dependencies change
- Test on Mac (system Chrome) before committing

### HTML Templates

- Keep mobile-responsive (320px minimum)
- Test on iOS Safari (common RedNote user device)
- Validate HTML before committing

## Maintenance Schedule

### Weekly
- Check core curriculum video links (11 videos)
- Verify DeepLearning.AI course links still active

### Monthly
- Full link audit (run commands above)
- Check for 404s in documentation links
- Verify GitHub repos still public

### Quarterly
- Review arXiv paper links
- Check for updated versions of resources
- Update FULL-LINK-AUDIT.md maintenance date

## Commit Messages

**Format:** `<type>: <description>`

**Types:**
- `fix:` - Broken link fixes, typo corrections
- `content:` - New lessons, resources, curriculum changes
- `docs:` - Documentation updates
- `style:` - CSS/design updates (no content change)
- `audit:` - Link audit updates

**Examples:**
- `fix: Update Anthropic agent-patterns links (11 files)`
- `fix: Correct YouTube video IDs (Day 1, 4, 16)`
- `content: Add Day 18 capstone project guide`
- `audit: Monthly link check - all 127 links verified`

## Pre-Commit Checklist

Before pushing:
- [ ] All links verified
- [ ] FULL-LINK-AUDIT.md updated
- [ ] No placeholder URLs (YOUR_USERNAME, example.com)
- [ ] No broken YouTube embeds
- [ ] Mobile responsive (if HTML/CSS changes)
- [ ] Commit message follows format

---

**Remember:** This course is used by real learners. Broken links = broken learning experience. Verify everything! 🔗✅
