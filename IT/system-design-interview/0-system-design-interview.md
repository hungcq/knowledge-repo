# System Design Interview

## Info
- Type: book
- Author: TODO

## Category
Practical, IT, System design

## Structure
- Foreword: intro problems, purpose of system design interview (SDI), goals of the book
- Chap 1: scaling techniques
- Chap 2: estimation techniques
- Chap 3: interview framework
- Chap 4-15: different design problems
- Chap 16: references of real world system

## Author's problems & solutions
- Problems: SDI is challenging:
  - SDI questions are big scoped & vague
  - SDI processes are open-ended without a standard/correct answer
- Goals:
  - Provide a reliable strats to approach the system design question
  - Provide solid knowledge in building a scalable system

## Presentation & styles

## Terms
- SLA: service level agreement, defining the uptime the service provider promises to deliver

## Criticisms
- Chap 6 assume leaderless replication models without acking it first
- Some concepts are a bit confusing (eg web server are used instead of API gateway in chapter 11)
- Chap 13 Feed service and Post service share the same Post cache & DB

## Takeaway
- Basic scaling techniques
- How to design popular systems (eg noti, chat)
- References to blogs/papers of actual system