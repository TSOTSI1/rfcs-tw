- Feature Name: leadership-council
- Start Date: 2022-08-01
- RFC PR: [rust-lang/rfcs#3392](https://github.com/rust-lang/rfcs/pull/3392)
- Rust Issue: N/A
- Commit: [The commit link this page based on](https://github.com/rust-lang/rfcs/blob/075f4b30f5c33315163c8e6a75e3210af6229ded/text/3392-leadership-council.md)

# 摘要

這份請求意見書（RFC）確立了一個領導理事會，作為核心團隊的繼任者[^core]和 Rust 專案的新治理結構，透過這個結構，Rust 專案成員共同授權[^authority]以確保專案的成功運作。領導理事會將大部分的權限委派給各個團隊（包括子團隊、工作小組等[^teams]），讓他們自主決策有關其範圍的事項。但理事會仍然保留一些決策權限，由這份請求意見書來明確和界定。

該理事會由從每個[高層團隊][top-level-teams] 中被委派為理事會代表的成員組成。

理事會負責整個 Rust 專案的成功。理事會將確立需要完成但尚未有明確負責人的工作，創建新的團隊來完成這些工作，監督現有團隊負責其範圍內的工作，並協調和調整專案團隊的組織結構。

# 大綱

- [參考資料](#參考資料)
- [動機](#動機)
- [理事會之職責、期待與限制](#理事會之職責、期待與限制)
- [理事會組織架構](#理事會組織架構)
  - [一級團隊單位](#一級團隊單位)
    - [一級團隊初始名單](#一級團隊初始名單)
    - [「啟動台」 一級團隊](#啟動台-一級團隊)
    - [廢除一級團隊](#廢除一級團隊)
  - [候補與放棄代表權利](#候補與放棄代表權利)
  - [任期限制](#任期限制)
  - [對單一公司或實體代表之限制](#對單一公司或實體代表之限制)
  - [候選資格](#候選資格)
  - [與 Core 團隊之關係](#與-core-團隊之關係)
  - [與 Rust 基金會之關係](#與-rust-基金會之關係)
- [理事會決策流程](#理事會決策流程)
  - [營運與政策決策](#營運與政策決策)
  - [重複與例外](#重複與例外)
  - [共識決策流程](#共識決策流程)
    - [核准標準](#核准標準)
  - [變更與調整決策流程](#變更與調整決策流程)
  - [議程與待辦事項](#議程與待辦事項)
  - [解決僵局](#解決僵局)
  - [回饋與評估](#回饋與評估)
- [決策流程之透明度和監督](#決策流程之透明度和監督)
  - [理事會可在內部做出之決定](#理事會可在內部做出之決定)
  - [理事會須私下保密做出之決定](#理事會須私下保密做出之決定)
  - [理事會須經公開提案做出之決定](#理事會須經公開提案做出之決定)
  - [利益衝突](#利益衝突)
  - [確定與更改團隊權責](#確定與更改團隊權責)
- [監督與問責機制](#監督與問責機制)
  - [確保能追究理事會之責任](#確保能追究理事會之責任)
  - [確保能追究理事會代表之責任](#確保能追究理事會代表之責任)
  - [確保能追究團隊之責任](#確保能追究團隊之責任)
- [審核、分歧與衝突](#審核、分歧與衝突)
  - [團隊間之分歧](#團隊間之分歧)
  - [涉及團隊或專案成員之衝突](#涉及團隊或專案成員之衝突)
  - [審核人代表團](#審核人代表團)
  - [審核團隊之政策與程序](#審核團隊之政策與程序)
  - [稽核](#稽核)
  - [最終問責機制](#最終問責機制)
  - [涉及專案成員之審核措施](#涉及專案成員之審核措施)
  - [涉及理事會代表之衝突](#涉及理事會代表之衝突)
  - [涉及審核團隊成員之衝突](#涉及審核團隊成員之衝突)
- [本案之批准](#本案之批准)
- [附註](#附註)

# 參考資料

To reduce the size of this RFC, non-binding reference materials appear in separate documents:

- [Full motivation](3392-leadership-council/motivation.md)
  - [Further research into the needs of Project-wide governance (Inside Rust blog post)](https://blog.rust-lang.org/inside-rust/2022/05/19/governance-update.html)
- [Non-goals of this RFC](3392-leadership-council/non-goals.md)
- [Rationale and alternatives](3392-leadership-council/alternatives.md)
- [Recommendations for initial work of the Council](3392-leadership-council/initial-work-of-the-council.md)

# 動機

Rust 專案由分布在全球的數百人組成，組織成擁有不同職責範圍的團隊。然而，許多工作超出了任何既有團隊的範圍，且仍然需要完成。

歷史上，核心團隊既辨識和優先處理落在團隊範圍之外的重要工作，也試圖自行完成這些工作。然而，將這兩種活動放在同一個團隊中無法擴展，反而會導致工作過度造成精疲力盡。

這份RFC確立的領導理事會專注於確定和優先處理團隊範圍之外的工作。理事會主要是授權其他人去完成工作，而不是自己親自去執行。理事會也可以充當各個團隊之間的協調、組織和負責任機構，例如跨團隊合作、路線圖以及項目的長期成功。

此RFC還建立了一系列監督和負責制度的機制，以協調整個委員會、各個委員會成員、管理團隊、項目團隊和項目成員之間的關係。

# 理事會之職責、期待與限制

高層級描述下，理事會**只**負責以下職責：

- 識別、優先排序以及追蹤由於缺乏明確負責者而無法執行的工作（而不應對負責者刻意降低優先度、置於待辦事項等的工作）。
- 委派該工作，並潛在可建立全新的（並可能為**暫時性的**）團隊來負責此工作。
- 為沒有明確負責者的**緊急**事項下達決策。
    - 此行為只能在特例情境下執行，即該決策無法委派給既有團隊也無法交付給全新團隊時。
- 為團隊、架構或流程協調橫跨專案的變更。
- 確保一級團隊能為其權責、對其他團隊以及對專案本身負責。
- 確保各個團隊能有完成其工作所需的人力與資源。
- 為 Rust 專案整體建立起官方的定位、觀點或意願。
    - 藉此能幫助降低橫跨專案的協調需求，尤其是面對長期公開投票與共識建立流程不夠實際的情境。舉例來說，要對第三方單位溝通 Rust 專案整體「 所想要的目標」時。

除了這些職責外，對理事會也有額外的期待與限制，以幫助判斷理事會是否正常運作：

- **委派工作**：理事會不應該主動執行本案沒有明確指派的工作；理事會必須委派給既有團隊或者成員與理事會不重複的全新團隊。執行工作的團隊中可以有理事會的代表，但是做為團隊成員並不屬於理事會代表的權責。
- **為了確保專案長期的流暢運作**：理事會應該要確保非緊急專案管理工作有接受優先度排序，並且能定期完成以確保專案不會累積成整個組織級別的負擔。
- **負責任**：由於理事會擁有廣泛的權力，理事會與理事會代表必須要為自己的行為負責任。他們應該要傾聽他人的回饋，並且能對他們是否可以繼續達到該職位所需的職責與期待進行主動的反思。
- **做好代表**：理事會代表不只要能代表整個專案各形式的考量，也要能盡可能代表 Rust 社群的各方面（人口分布、技術背景等等）。
- **共享負擔**：所有理事會代表都必須共享理事會職責的負擔。
- **尊重他人的權責**：理事會必須尊重委派給各團隊的權責。理事會必須與各團隊諮商並且共同合作解決問題，並且盡量不作出違背任何團隊意願的決策。
- **以良善原則行事**：理事會代表應該以 Rust 專案**整體**的利益作出決策，即便這些決策可能會與各個團隊、雇主以及其他外部單位的利益衝突。
- **保持透明**：雖然不是所有決策（以及決策的各方面）都能被公開，理事會應該要盡可能維持其決策的公開與透明。理事會也應該要確保專案的組織架構很明確透明。
- **尊重隱私**：理事會的成員絕不能為了透明性而洩漏個人或者機密情報，包含可能會意外洩漏重要資訊的周邊資訊。
- **維持健康的工作環境**：理事會代表應該要為他們的貢獻與其性質感到滿意。他們不應認為自己在理事會中的存在只是義務所為，而必須是因為他們用有意義的方式主動參與。
- **持續演化**：理事會受到期待會隨著時間演化以應對團隊、專案以及社群的演化。

理事會代表、審核團隊成員以及其他專案成員都應該能為身邊的人以及更廣泛的社群做好示範。這些職位都有對應的責任與領導，也因此這些人的行為都帶有份量而會對社群造成重大影響，也因此必須注意行使職權。選擇要行使這些職權的人都應該要知道身邊的人會以對應的高標準看待他們。

# 理事會組織架構

理事會由一群團隊代表所組成，各代表一支[一級團隊][top-level-teams]以及其子團隊。

每支一級團隊都能用各自所選的程序選出恰好一名代表。

任何一級團隊的成員或其子團隊的成員都能作為其代表。團隊必須提供子團隊成員對潛在候選給予意見與回饋的經驗。

各個代表最多代表一支一級團隊，就算他們也是其他團隊的成員。代表任何 Rust 團隊的主要責任將由其所屬的一級團隊代表負責。[^under-multiple-teams]

所有 Rust 專案團隊都必須至少隸屬於一支一級團隊。對於目前沒有母團隊的團隊，本案會建立起[「啟動台團隊」][launching-pad]作為暫時性的隸屬對象。以確保所有團隊都在理事會有對應的代表。

## 一級團隊單位
[top-level-teams]: #一級團隊單位

理事會將會透過公開政策決策建立一級團隊。一般來說，一級團隊應該要符合以下條件：
- 有對 Rust 專案具備根本重要性的權責
- 是該權責全面向的最終決策者
- 所有權責不隸屬於其他團隊權責（不能為子團隊或相似管理架構所有）
- 有著能期待無止盡持續的開放權責
- 目前為 Rust 專案中活躍的存在

一級團隊的數量必須介於 4 到 9（包含）之間，傾向介於 5 到 8 之間。這個數字能相對平衡多元性的需求以及相對小的架構，同時又在進行有效對話與共識凝聚時具備實務性。[^number-of-representatives]

當理事會建立起全新一級團隊時，該團隊則該指派一名理事會代表。[^bootstrapping-new-teams]當建立起全新的一級團隊時，理事會必須提供為何該一級團隊不能作為子團隊或者其他管理架構存在的解釋。

### 一級團隊初始名單

一級團隊的初始名單由本案使發表時列於 [rust-lang.org 網站的一級管理區域](https://www.rust-lang.org/governance)的所有團隊組成（除去 Core 團隊與校友），再加上[「啟動台」團隊][launching-pad]：
- 編譯器
- Crates.io
- 開發工具
- 基礎架構
- 語言
- 啟動台
- 函式庫
- 審核
- 發佈

本清單並不是最佳的一級團隊組成。本案建議理事會的最開始的工作就是檢視既存的管理架構並確保所有架構都在一個或多個一級團隊中有直接或間接的代表，並且確保所有一級團隊都有符合能被認定為一級團隊的條件。這將會涉及對一級團隊組成的調整。

### 「啟動台」一級團隊
[launching-pad]: #「啟動台」一級團隊

本案會建立「啟動台（launching pad）」團隊以**暫時**接受沒有對應一級團隊可以歸類的子團隊。這樣能夠確保在更加永久性的母團隊被找到或者建立起之前，所有團隊都在理事會有代表。

「啟動台」是個雨傘團隊：該團隊沒有直接成員，只有子團隊代表。

理事會應該要致力於為所有「啟動台」子團隊找尋或者建立更合適的母團隊，並且隨之將子團隊移轉至對應的母團隊。

在某些情況下，雖有合適的母團隊但尚未準備好接受子團隊時，啟動台能作為臨時歸宿容納這些例子。

而對於團隊面臨移除或重組時，如果移除或重組時並沒有明確將其子團隊納入其他組織中的母團隊，則啟動台將會作為這些子團隊的預設歸宿。

理事會必須每六個月審視「啟動台」中的子團隊成員狀況，以確保有合適的流程在協助所有子團隊成員找到新的母團隊。而與其它一級團隊相同的是，只要理事會認為「啟動台」團隊不再需要，就可以將之撤除（並且移除掉其在理事會中的代表）。撤除「啟動台」團隊的流程與其他一級團隊同理。除此之外，理事會也可以給予「啟動台」團隊自己的權責，但是此措施不屬於本案的範圍內。

### 廢除一級團隊

任何要移除團隊的一級指定（或其他會導致無法參與理事會）的決策，都需要除卻將被移除的一級團隊代表外所有理事會代表的共識。雖然如此，必須要邀請考慮移除的團隊代表參與關於團隊移除的理事會審議，而理事會也只能在極端特例下不顧團隊反對將之移除。

理事會不得移除審核團隊。理事會不能在沒有審核團隊的同意下改變審核團隊的權責。

## 候補與放棄代表權利

A representative may end their term early if necessary, such as due to changes in their availability or circumstances. The respective top-level team must then begin selecting a new representative. The role of representative is a volunteer position. No one is obligated to fill that role, and no team is permitted to make serving as a representative a necessary obligation of membership in a team. However, a representative is obligated to fulfill the duties of the position of representative, or resign that position.

A top-level team may decide to temporarily relinquish their representation, such as if the team is temporarily understaffed and they have no willing representative. However, if the team does not designate a Council representative, they forgo their right to actively participate in decision-making at a Project-wide level. All Council procedures including decision-making should not be blocked due to this omission. The Council is still obligated to consider new information and objections from all Project members. However, the Council is not obligated to block decisions to specially consider or collate a non-represented team's feedback.

Sending a representative to the Council is considered a duty of a top-level team, and not being able to regularly do so means the team is not fulfilling its duties. However, a Council representative does not relinquish their role in cases of short absence due to temporary illness, vacation, etc.

A top-level team can designate an alternate representative to serve in the event their primary representative is unavailable. This alternate assumes the full role of Council representative until the return of the primary representative. Alternate representatives do not regularly attend meetings when the primary representative is present (to avoid doubling the number of attendees).

If a team's representative *and* any alternates fail to participate in any Council proceedings for 3 consecutive weeks, the team's representative ceases to count towards the decision-making quorum requirements of the Council until the team can provide a representative able to participate. The Council must notify the team of this before it takes effect. If a team wishes to ensure the Council does not make decisions without their input or without an ability for objections to be made on their behalf, they should ensure they have an alternate representative available.

A top-level team may change their representative before the end of their term, if necessary.  However, as maintaining continuity incurs overhead, teams should avoid changing their representatives more than necessary. Teams have the primary responsibility for briefing their representative and alternates on team-specific issues or positions they wish to handle on an ongoing basis. The Council and team share the responsibilities of maintaining continuity for ongoing issues within the Council, and of providing context to alternates and other new representatives.

For private matters, the Council should exercise discretion on informing alternates, to avoid spreading private information unnecessarily; the Council can brief alternates if they need to step in.

## 任期限制

理事會代表任期為一年。對於任何已被認可的代表團（來自特定一級團隊的代表團），每位代表有最多連任三次的非硬性限制。一位代表在理事會收到來自個別團隊明確指出他們無法產生另一位代表時，得超過任期限制（舉例來說，因為缺乏其他有意願的候選人，或是因為團隊成員對其他任何候選人提出反對意見）。

除此之外，對於單一代表在其他一級團隊服務的任期數、或是在單一一級團隊的非連續任期，並沒有任何硬性限制。團隊應該力求在經驗的存續與代表的替換之間取得平衡，以提供更多人這樣的經驗。[^representative-selection]

一半的代表將在（每年的）三月底進行任命，另一半則在九月底進行任命。這避免了同時更換所有理事會代表。對於初始的理事會以及在任何時候的一級團隊組成發生改變，理事會以及一級團隊應該共同努力使任期結束日大約平均落在在三月與九月各半。然而，每個任期應該至少持續六個月（為了避免任期過短，暫時的不平衡是可被接受的）。

如果理事會及一級團隊無法就適當的任期結束日變更達成共識，代表將在三月底或九月底兩者之間被隨機分配一個任期結束日（且在至少 6 個月後）以維持平衡。

## 對單一公司或實體代表之限制

Council representatives must not disproportionately come from any one company, legal entity, or closely related set of legal entities, to avoid impropriety or the appearance of impropriety. If the Council has 5 or fewer representatives, no more than 1 representative may have the same affiliation; if the Council has 6 or more representatives, no more than 2 representatives may have the same affiliation.

Closely related legal entities include branches/divisions/subsidiaries of the same entity, entities connected through substantial ownership interests, or similar. The Council may make a judgment call in unusual cases, taking care to avoid conflicts of interest in that decision.

A Council representative is affiliated with a company or other legal entity if they derive a substantive fraction of their income from that entity (such as from an employer, client, or major sponsor). Representatives must promptly disclose changes in their affiliations.

If this constraint does not hold, whether by a representative changing affiliation, top-level teams appointing new representatives, or the Council size changing, restore the constraint as follows:
- Representatives with the same affiliation may first attempt to resolve the issue amongst themselves, such that a representative voluntarily steps down and their team appoints someone else.
  - This must be a decision by the representative, not their affiliated entity; it is considered improper for the affiliated entity to influence this decision.
  - Representatives have equal standing in such a discussion; factors such as seniority in the Project or the Council must not be used to pressure people.
- If the representatives with that affiliation cannot agree, one such representative is removed at random. (If the constraint still does not hold, the remaining representatives may again attempt to resolve the issue amongst themselves before repeating this.) This is likely to produce suboptimal results; a voluntary solution will typically be preferable.
- While a team should immediately begin the process of selecting a successor, the team's existing representative may continue to serve up to 3 months of their remaining term.
- The existing representative should coordinate the transition with the incoming representative but it is the team's choice which one is an actual representative during the up to 3 month window. There is only ever one representative from the top-level team.

## 候選資格

以下是決定理想候選人的標準，這些標準雖類似團隊領導者或共同領導者的標準，但並不完全相同。儘管團隊領導者**可能**也能成為傑出的理事會代表，但擔任團隊領導者和委員會代表都需要大量時間投入，這會促使將這些角色分配給不同的人。這些標準並非硬性要求，但可用於決定誰最適合成為團隊代表。簡而言之，代表應具備以下條件：
- 有充沛的時間與精力，以滿足委員會的需求。
- 有興趣協助處理專案營運和治理相關事務。
- 廣泛了解專案的需求，且不限於其所在團隊或積極貢獻之領域。
- 對自己的團隊需求有敏銳的感知。
- 具備代表他人的氣質和能力，超越任何私人事務。
- 能夠代表其團隊的所有觀點，不僅僅是部分觀點，也不僅僅是團隊成員同意的觀點。

儘管有些團隊目前可能沒有足夠的候選人符合這些標準，委員會應積極培養這些技能之人才，因為這些技能不僅對委員會成員資格有幫助，也對這個專案有益。

## 與 Core 團隊之關係

The Leadership Council serves as the successor to the core team in all capacities. This RFC was developed with the participation and experience of the core team members, and the Council should continue seeking such input and institutional memory when possible, especially while ramping up.

External entities or processes may have references to "the Rust core team" in various capacities. The Council doesn't use the term "core team", but the Council will serve in that capacity for the purposes of any such external references.

## 與 Rust 基金會之關係

The Council is responsible for establishing the process for selecting Project directors. The Project directors are the mechanism by which the Rust Project's interests are reflected on the Rust Foundation board.

The Council delegates a purview to the Project directors to represent the Project's interests on the Foundation Board and to make certain decisions on Foundation-related matters. The exact boundaries of that purview are out of scope for this RFC.

# 理事會決策流程
[decision-making]: #the-council-s-decision-making-process

The Leadership Council make decisions of two different types: operational decisions and policy decisions. Certain considerations may be placed on a given decision depending on its classification. However, by default, the Council will use a consent decision-making process for all decisions regardless of classification.

## 營運與政策決策

Operational decisions are made on a daily basis by the Council to carry out their aims, including regular actions taking place outside of meetings (based on established policy). Policy decisions provide general reusable patterns or frameworks, meant to frame, guide, and support operations. In particular, policy decisions can provide partial automation for operational decisions or other aspects of operations. The council defaults to the consent decision making process for all decisions unless otherwise specified in this RFC or other policy.

This RFC does not attempt to precisely define which decisions are operations versus policy; rather, they fall somewhere along a continuum. The purpose of this distinction is not to direct or constrain the council's decision-making procedures. Instead, this distinction provides guidance to the Council, and clarifies how the Council intends to record, review, and refine its decisions over time. For the purposes of any requirements or guidance associated with the operational/policy classification, anything not labeled as either operational or policy in this or future policy defaults to policy. 

## 重複與例外
[repetition-and-exceptions]: #repetition-and-exceptions

Policy decisions often systematically address what might otherwise require repeated operational decisions. The Council should strive to recognize when repeated operational decisions indicate the need for a policy decision, or a policy change. In particular, the Council should avoid allowing repeated operational decisions to constitute de facto policy.

Exceptions to existing policy cannot be made via an operational decision unless such exceptions are explicitly allowed in said policy. Avoiding ad-hoc exceptions helps avoid ["normalization of deviance"](https://en.wikipedia.org/wiki/Normalization_of_deviance).

## 共識決策流程

The Council will initially be created with a single process for determining agreement to a proposal. It is however expected that the Council will add additional processes to its toolbox soon after creation.

Consent means that no representative's requirements (and thus those of the top-level team and subteams they represent) can be disregarded. The Council hears all relevant input and sets a good foundation for working together equitably with all voices weighted equally.

The Council uses consent decision-making where instead of being asked "do you agree?", representatives are asked "do you object?". This eliminates "pocket vetoes" where people have fully reviewed a proposal but decide against approving it without giving clear feedback as to the reason. Concerns, feedback, preferences, and other less critical forms of feedback do not prevent making a decision, but should still be considered for incorporation earlier in drafting and discussion. Objections, representing an unmet requirement or need, *must* be considered and resolved to proceed with a decision.

### 核准標準

The consent decision-making process has the following approval criteria:
- Posting the proposal in one of the Leadership Council's designated communication spaces (a meeting or a specific channel).
- Having confirmation that at least N-2 Council representatives (where N is the total number of Council representatives) have fully reviewed the final proposal and give their consent.
- Having no outstanding explicit objections from any Council representative.
- Providing a minimum 10 days for feedback.

The approval criteria provides a quorum mechanism, as well as sufficient time for representatives to have seen the proposal. Allowing for two non-signoffs is an acknowledgement of the volunteer nature of the Project, based on experience balancing the speed of decisions with the amount of confirmation needed for consent and non-objection; this assumes that those representatives have had time to object if they wished to do so. (This is modeled after the process used today for approval of RFCs.)

The decision-making process can end at any time if the representative proposing it decides to retract their proposal. Another representative can always adopt a proposal to keep it alive.

If conflicts of interest result in the Council being unable to meet the N-2 quorum for a decision, the Council cannot make that decision unless it follows the process documented in [the "Conflicts of interest" section for how a decision may proceed with conflicts documented][conflicts-of-interest]. In such a case, the Council should consider appropriate processes and policies to avoid future recurrences of a similar conflict.

## 變更與調整決策流程

Using the public policy process, the Council can establish different decision-making processes for classes of decisions.

For example, the Council will almost certainly also want a mechanism for quick decision-making on a subset of operational decisions, without having to wait for all representatives to affirmatively respond. This RFC doesn't define such a mechanism, but recommends that the Council develop one as one of its first actions.

When deciding on which decision-making process to adopt for a particular class of decision, the Council balances the need for quick decisions with the importance of confidence in full alignment. Consent decision-making processes fall on the following spectrum:

- Consensus decision making (prioritizes confidence in full alignment at the expense of quick decision making): team members must review and prefer the proposal over all others, any team members may raise a blocking objection
- Consent decision making (default for the Council, balances quick decisions and confidence in alignment): team members must review and may raise a blocking objection
- One second and no objections (prioritizes quick decision making at the expense of confidence in alignment): one team member must review and support, any team member may raise a blocking objection

Any policy that defines decision-making processes must at a minimum address where the proposal may be posted, quorum requirements, number of reviews required, and minimum time delay for feedback. A lack of objections is part of the approval criteria for all decision-making processes.

If conflicts of interest prevent more than a third of the Council from participating in a decision, the Council cannot make that decision unless it follows the process documented in [the "Conflicts of interest" section for how a decision may proceed with conflicts documented][conflicts-of-interest]. (This is true regardless of any other quorum requirements for the decision-making process in use.) In such a case, the Council should consider appropriate processes and policies to avoid future recurrences of a similar conflict.

The Council may also delegate subsets of its own decision-making purviews via a public policy decision, to teams, other governance structures, or roles created and filled by the Council, such as operational lead, meeting facilitator, or scribe/secretary.

Note that the Council may delegate the drafting of a proposal without necessarily delegating the decision to approve that proposal. This may be necessary in cases of Project-wide policy that intersects the purviews of many teams, or falls outside the purview of any team. This may also help when bootstrapping a new team incrementally.

## 議程與待辦事項

The Council's agenda and backlog are the primary interface through which the Council tracks and gives progress updates on issues raised by Project members throughout the Project.

To aid in the fairness and effectiveness of the agenda and backlog, the Council must:

- Use a tool that allows Project members to submit requests to the Council and to receive updates on those requests.
- Use a transparent and inclusive process for deciding on the priorities and goals for the upcoming period. This must involve regular check-ins and feedback from all representatives.
- Strive to maintain a balance between long-term strategic goals and short-term needs in the backlog and on the agenda.
- Be flexible and adaptable and be willing to adjust the backlog and agenda as needed in response to changing circumstances or priorities.
- Regularly review and update the backlog to ensure that it accurately reflects the current priorities and goals of the Council.
- Follow a clear and consistent process for moving items from the backlog to the agenda, such as delegating responsibility to roles (e.g. meeting facilitator and scribe), and consenting to the agenda at the start of meetings. Any agenda items rejected during the consent process must have their objections documented in the published meeting minutes of the Council.

## 解決僵局

In some situations the Council might need to make an decision urgently and not feel it can construct a proposal in that time that everyone will consent to. In such cases, if everyone agrees that a timely decision they disagree with would be a better outcome than no timely decision at all, the Council may use an alternative decision-making method to attempt to resolve the deadlock. The alternative process is informal, and the council members must still re-affirm their consent to the outcome through the existing decision making process. Council members may still raise objections at any time.
 
For example, the Council can consent to a vote, then once the vote is complete all of the council members would consent to whatever decision the vote arrived to. The Council should strive to document the perceived advantages and disadvantages for choosing a particular alternative decision-making model.

There is, by design, no mandatory mechanism for deadlock resolution. If the representatives do not all consent to making a decision even if they don't prefer the outcome of that decision, or if any representative feels it is still possible to produce a proposal that will garner the Council's consent, they may always maintain their objections.

If a representative withdraws an objection, or consents to a decision they do not fully agree with (whether as a result of an alternative decision-making process or otherwise), the Council should schedule an evaluation or consider shortening the time until an already scheduled evaluation, and should establish a means of measuring/evaluating the concerns voiced. The results of this review are intended to determine whether the Council should consider changing its prior decision.

## 回饋與評估

All policy decisions should have an evaluation date as part of the policy. Initial evaluation periods should be shorter in duration than subsequent evaluation periods. The length of evaluation periods should be adjusted based on the needs of the situation. Policies that seem to be working well and require few changes should be extended so less time is spent on unnecessary reviews. Policies that have been recently adjusted or called into question should have shortened evaluation periods to ensure they're iterating towards stability more quickly. The Council should establish standardized periods for classes of policy to use as defaults when determining periods for new policy. For instance, roles could have an evaluation date of 3 months initially then 1 year thereafter, while general policy could default to 6 months initially and 2 years thereafter.

- New policy decisions can always modify or replace existing policies.
- Policy decisions must be published in a central location, with version history.
- Modifications to the active policy docs should include or link to relevant context for the policy decision, rather than expecting people to find that context later.

# 決策流程之透明度和監督

Decisions made by the Leadership Council will necessarily require varying levels of transparency and oversight based on the kind of decision being made. This section gives guidance on how the Council will seek oversight for its decisions, and what qualifies decisions to be made in private or in public.

This RFC places certain decisions into each category. All decisions not specifically enumerated must use the public policy process. The Council may evolve the categorization through the [public policy process](decisions-that-the-Council-must-make-via-public-proposal).

Decisions made by the Council fall into one of three categories, based on the level of oversight possible and necessary:

- Decisions that the Council may make internally
- Decisions that the Council must necessarily make privately
- Decisions that the Council must make via public proposal

## 理事會可在內部做出之決定

Some types of operational decisions can be made internally by the Council, with the provision that the Council has a mechanism for community feedback on the decision after it has been made.

Adding a new decision to the list of decisions the Council can make internally requires a public policy decision. Any decisions that impact the structure, decision-makers, or oversight of the Council itself should not be added to this list.

The Council should also strive to avoid establishing de facto unwritten policy via repeated internal decisions in an effort to avoid public proposal. See ["Repetition and exceptions"][repetition-and-exceptions] for more details.

This list exhaustively enumerates the set of decisions that the Council may make internally:

- Deciding to start a process that itself will play out in public (e.g. "let's start developing and posting the survey", "let's draft an RFC for this future public decision").
- Expressing and communicating an official position statement of the Rust Project.
- Expressing and communicating the position of the Rust Project directly to another entity, such as the Rust Foundation.
- Communicating via Rust Project communication resources (via the blog or all@).
- Making most operational decisions about the Council's own internal processes, including how the Council coordinates, the platforms it uses to communicate, where and when it meets, templates used for making and recording decisions (subject to requirements elsewhere in this RFC).
- Appointing officers or temporary roles within the Council, for purposes such as leading/facilitating meetings, recording and publishing minutes, obtaining and collating feedback from various parties, etc.[^council-roles] Note that any such roles (titles, duties, and current holders) must be publicly disclosed and documented.
- Inviting specific attendees other than Council representatives to specific Council meetings or discussions, or holding a meeting open to the broader community. (In particular, the Council is encouraged to invite stakeholders of a particular decision to meetings or discussions where said decision is to be discussed.)
- Making decisions requested by one or more teams that would be within the normal purviews of those teams to make without a public proposal. (Note that teams can ask for Council input without requesting a Council decision.)
- Making one-off judgment calls in areas where the purviews of teams overlap or are ambiguous (though *changing* the purviews of those teams must be a public policy decision).
- Any decision that this RFC or future Council policy specifies as an operational decision.

See the [accountability section][accountability] for details on the feedback mechanism for Council decisions.

## 理事會須私下保密做出之決定

Some decisions necessarily involve private details of individuals or other entities, and making these details public would have a negative impact both on those individuals or entities (e.g. safety) and on the Project (eroding trust).

This additional constraint should be considered an exceptional case. This does not permit making [decisions that would require a public proposal per the next section][decisions-that-the-Council-must-make-via-public-proposal]. However, this does permit decisions that the Council makes internally to be kept private, without full information provided for public oversight.

The Council may also decline to make a decision privately, such as if the Council considers the matter outside their purview (and chooses to defer to another team) or believes the matter should be handled publicly. However, even in such a case, the Council still cannot publicly reveal information shared with it in confidence (since otherwise the Council would not be trusted to receive such information). Obvious exceptions exist for imminent threats to safety.

Private decisions must not establish policy. The Council should also strive to avoid establishing de facto unwritten policy via repeated private decisions in an effort to avoid public proposal. See ["Repetition and exceptions"][repetition-and-exceptions] for more details.

This list exhaustively enumerates the set of decisions that the Council may make either partly or entirely in private:

- Determining relationships with new industry / Open Source initiatives, that require confidentiality before launching.
- Discussing the personal aspects of a dispute between teams that involves some interpersonal dynamics/conflicts.
- Participating in contract negotiations on behalf of the Project with third parties (e.g. accepting resources provided to the Project).
- Decisions touching on Project-relevant controversial aspects of politics, personal safety, or other topics in which people may not be safe speaking freely in public.
- Discussing whether and why a team or individual needs help and support, which may touch on personal matters.
- Any decision that this RFC or future Council policy specifies as a private decision.

The Council may pull in members of other teams for private discussions leading to either a private or public decision, unless doing so would more broadly expose private information disclosed to the Council without permission. When possible, the Council should attempt to pull in people or teams affected by a decision. This also provides additional oversight.

Some matters may not be fit for full public disclosure while still being fine to share in smaller, more trusted circles (such as with all Project members, with team leads, or with involved/affected parties). The Council should strive to share information with the largest appropriate audiences for that information.

The Council may decide to withhold new decisions or aspects of decisions when it's unclear whether the information is sensitive. However, as time progresses and it becomes clearer who the appropriate audience is or that the appropriate audience has expanded, the council should revisit its information-sharing decisions.

The Council should always loop in the moderation team for matters involving interpersonal conflict/dispute, both because such matters are the purview of the moderation team, and to again provide additional oversight.

The council should evaluate which portions of a decision or its related discussions necessarily need to be private, and should consider whether it can feasibly make non-sensitive portions public, rather than keeping an entire matter private just because one portion of it needs to be. This may include the existence of the discussion, or the general topic, if those details are not themselves sensitive.

Private matters may potentially be able to become public, or partially public, at a later date if they're no longer sensitive. However, some matters may potentially *never* be able to become public, which means they will never become subject to broader review and oversight. Thus, the Council must exercise caution and prudence before making a private decision.

The Council should make every effort to not make private decisions. The Council should have appropriate additional processes in place to encourage representatives to collectively review such decisions and consider their necessity.

## 理事會須經公開提案做出之決定
[decisions-that-the-Council-must-make-via-public-proposal]: #decisions-that-the-Council-must-make-via-public-proposal

Decisions in this category require the Council to publicly seek feedback from the broader Rust Project *in advance* of the decision being made. Such decisions are proposed and decided via the appropriate public decision process, currently the RFC process (though the Council may adopt a different public proposal process in the future). The public decision process must require the consent of representatives (either affirmatively or via non-objection), must allow for blocking objections by Council representatives, must provide reasonable time for public evaluation and discussion, and must provide a clear path for public feedback to the Council. 

Following the existing RFC process, public proposals must have a minimum time-delay for feedback before the decision takes effect. Any representative may request that the feedback period for a particular decision is extended to at most 20 days total. The Council may make an internal operational decision to extend the feedback period beyond 20 days. The time-delay for feedback starts only when the necessary threshold for approval is otherwise met, including there not being any raised objections. If objections are raised and resolved during the time-delay, the waiting period starts again.

The Leadership Council is expected to evolve over time to meet the evolving needs of the teams, the Rust Project, and the community. Such evolutionary changes may be small or large in scope and require corresponding amounts of oversight. Changes that materially impact the shape of the Council would need to be part of a public decision process.

As an exception to the above, modifications or removals of a single top-level team (other than the moderation team) may occur with the unanimous agreement of the Council absent the representative delegated by that top-level team.

The Council is permitted to have private *discussions* even on something that ultimately ends up as a public proposal or a publicly disclosed internal decision. The Council may wish to do this if the discussions are sensitive to allow decision participants to speak more frankly and freely. Additionally, in some cases, private information that can't be disclosed may impact an otherwise public decision/proposal; the Council should strive to be as transparent and non-misleading as possible and avoid having opaque decisions where all rationale is private.

Note that all decisions fall into this category unless explicitly designated (via this RFC or future public proposals) to fall into another category, so this list (unlike those in the other two categories) is intentionally vague/broad: it is intended to give guidance on what likely should belong in this category without necessarily being prescriptive.

- Any decision that has the effect of modifying the list of decision-makers on the Leadership Council or the decision-making process of the Leadership Council. For instance:
    - Changing this list (or this RFC in general).
    - Modifying the publication and approval process used for the Council's public proposals. Such a proposal must use the existing established process, not the proposed process.
    - Adding, modifying, or removing policies affecting eligibility for Council representatives.
    - Adding, modifying, or removing one or more top-level teams. This includes:
        - modifying the purview of a top-level team to such an extent that it meaningfully becomes a different team.
        - reorganizing the Project such that top-level teams move underneath other teams.
    - Adding other types of Council representatives other than those delegated by top-level teams.
    - Adding, modifying, or removing policies regarding Council quorums or the locations in which binding decisions can be made.
- Any policy decision, as opposed to a one-off operational decision. (See the [decision-making section][decision-making] for details on policy decisions versus operational decisions.) This includes any decision that binds the decisions of other parts of the Project (e.g. other teams or individuals), effectively serving as an exception to the normal purviews of all teams. Some examples of policy decisions:
    - Modifying or extending existing policies, including those previously made via RFC.
    - A legal/licensing policy affecting Rust Project software or other work of the Rust Project.
    - A change to the Code of Conduct.
    - A policy affecting eligibility for membership in the Rust Project or any team thereof.
    - A change to how the moderation team moderates Council representatives or the Leadership Council as a whole. Such decisions must be made jointly with the moderation team.
    - An agreement with another project or organization that makes any ongoing commitments on behalf of the Rust Project. (One-off commitments involving teams that have agreed to those commitments are fine.)
    - Creating or substantially modifying legal structures (e.g. additional Foundations, changing relationship with the Rust Foundation, partnering with other legal entities).
    - Making policy decisions requested by one or more teams that would be within the normal purviews of those teams. (Note that teams can ask for Council input without requesting a Council decision.)
    - Deciding that a class of future decisions always belongs within the Council, rather than being delegated to any other team.
- Any decision that this RFC or future Council policy specifies as a public policy decision.

## 利益衝突
[conflicts-of-interest]: #conflicts-of-interest

A Council representative must not take part in or influence a decision in which they have a conflict of interest.

Potential sources of conflicts of interest include, but are not limited to:
- Personal: a decision about themselves
- Financial: a decision with any substantive financial impact on the representative
- Employment or equivalent: a decision involves another person at the same company, or would benefit/harm that company disproportionately more than others
- Professional or other affiliation: a decision involves an organization the representative is associated with, such as an industry/professional/standards/governmental organization
- Familial/Friendship: a decision about a person the representative cannot be expected to be impartial about, including a conflict of interest of another type through that person (such as a family member's business)

Council representatives must promptly disclose conflicts of interest and recuse themselves from affected decisions. Council representatives must also proactively disclose likely sources of potential conflict annually to other representatives and to the moderation team.

Note that conflicts of interest can arise even if a proposal does not name a specific entity. Council representatives cannot, for instance, use their position to tailor requirements in a proposal to disproportionately benefit their employer.

A proposal favored widely across the Rust community does not automatically represent a conflict of interest for a representative merely because that representative's employer or equivalent also favors the general area of that proposal, as long as the proposal does not favor any particular entities. For example, a proposal to improve the security of a particular Rust component is not a conflict of interest for representatives just because their employers generally care about Rust security; however, a proposal to engage specific developers or security experts, or one's compensation being predicated on such a proposal, might still raise a conflict.

The Council may not waive a conflict of interest if one applies, even if the Council considers it minor. However, the Council may evaluate *whether* a conflict exists at all. Council representatives must raise potential conflicts so that the Council can make such a determination.

The Council may request specific information from a recused representative, and the recused representative may provide that information upon request.

Where possible and practical, the Council should separate decisions to reduce the scope of a conflict of interest. For instance, the Council could separate a decision to arrange access to a class of hardware (without setting specific requirements or selecting vendors) from the decision of which exact hardware to purchase and where to purchase it, if doing so made a conflict of interest only apply to the latter decision.

A representative simultaneously considering the interests of the Rust Project and the interests of any Project team is not necessarily a conflict of interest. In particular, representatives are *expected* to regularly take part in decisions involving their teams, as delegates from those teams.

In the unlikely event that a proposed decision produces a conflict of interest with enough representatives that the remainder cannot meet a previously established quorum requirement, and the decision must still be made, then either top-level teams must provide alternate representatives for the purposes of the specific decision, or (for public decisions only) the Council may elect to proceed with the decision while publicly documenting all conflicts of interest. (Note that proceeding with a public decision, even with conflicts documented, does not actually eliminate the conflicts or prevent them from influencing the decision; it only allows the public to judge whether the conflicts might have influenced the decision. Eliminating the conflicts entirely is always preferable.) In such a case, the Council should consider appropriate processes and policies to avoid future recurrences of a similar conflict.

## 確定與更改團隊權責

The Council can move an area or activity between the purviews of top-level teams either already existing or newly created (other than the moderation team). Though the purview of a given top-level team may be further sub-divided by that team, the Council only moves or adjusts top-level purviews. If a sub-divided purview is moved, the Council will work with the involved teams to coordinate the appropriate next steps. This mechanism should be used when the Council believes the existing team's purview is too broad, such that it is not feasible to expect the team to fulfill the full purview under the current structure.  However, this should not happen when a team only *currently* lacks resources to perform part of its duties.

The Council also must approve expansions of a top-level team's purview, and must be notified of reductions in a top-level team's purview. This most often happens when a team self-determines that they wish to expand or reduce their purview. This could also happen as part of top-level teams agreeing to adjust purviews between themselves. Council awareness of changes to a purview is necessary, in part, to ensure that the purview can be re-assigned elsewhere or intentionally left unassigned by the Council.

However, teams (individually or jointly) may further delegate their purviews to subteams without approval from the Council. Top-level teams remain accountable for the full purviews assigned to them, even if they delegate (in other words, teams are responsible for ensuring the delegation is successful).

The Council should favor working with teams on alternative strategies prior to shifting purviews between teams, as this is a relatively heavyweight step. It's also worth noting that one of the use cases for this mechanism is shifting a purview previously delegated to a team that functionally no longer exists (for instance, because no one on the team has time), potentially on a relatively temporary basis until people arrive with the time and ability to re-create that team. This section of the RFC intentionally does not put constraints on the Council for exactly how (or whether) this consultation should happen.

# 監督與問責機制
[accountability]: #mechanisms-for-oversight-and-accountability

The following are various mechanisms that the Council uses to keep itself and others accountable.

## 確保能追究理事會之責任

The Council must publicly ensure that the wider Project and community's expectations of the Council are consistently being met. This should be done both by adjusting the policies, procedures, and outcomes of the Council as well as education of the Project and community when their expectations are not aligned with the reality.

To achieve this, in addition to rotating representatives and adopting a "public by default" orientation, the Council must regularly (at least on a quarterly basis) provide some sort of widely available public communication on their activities as well as an evaluation of how well the Council is functioning using the list of duties, expectations, and constraints as the criteria for this evaluation.

Each year, the Council must solicit feedback on whether the Council is serving its purpose effectively from all willing and able Project members and openly discuss this feedback in a forum that allows and encourages active participation from all Project members. To do so, the Council and other Project members consult the high-level duties, expectations, and constraints listed in this RFC and any subsequent revisions thereof to determine if the Council is meeting its duties and obligations.

In addition, it is every representative's *individual* responsibility to watch for, call out, and refuse to go along with failures to follow this RFC, other Council policies and procedures, or any other aspects of Council accountability. Representatives should strive to actively avoid ["diffusion of responsibility"](https://en.wikipedia.org/wiki/Diffusion_of_responsibility), the phenomenon in which a group of people collectively fail to do something because each individual member (consciously or subconsciously) believes that someone else will do so. The Council may also wish to designate a specific role with the responsibility of handling and monitoring procedural matters, and in particular raising procedural points of order, though others can and should still do so as well.

If any part of the above process comes to the conclusion that the Council is *not* meeting its obligations, then a plan for how the Council will change to better be able to meet their obligations must be presented as soon as possible. This may require an RFC changing charter or similar, a rotation of representatives, or other substantive changes. Any plan should have concrete measures for how the Council and/or Rust governance as a whole will evolve in light of the previous year's experience.

## 確保能追究理事會代表之責任

Council representatives should participate in regular feedback with each other and with their respective top-level team (the nature of which is outside the scope of this RFC) to reflect on how well they are fulfilling their duties as representatives. The goal of the feedback session is to help representatives better understand how they can better serve the Project. This feedback must be shared with all representatives, all members of the representative's top-level team, and with the moderation team. This feedback should ask for both what representatives have done well and what they could have done better.

Separately, representatives should also be open to private feedback from their teams and fellow representatives at any time, and should regularly engage in self-reflection about their role and efficacy on the Council.

Artifacts from these feedback processes must never be made public to ensure a safe and open process. The Council should also reflect on and adjust the feedback process if the results do not lead to positive change.

If other members of the Council feel that a Council representative is not collaborating well with the rest of the Council, they should talk to that representative, and if necessary to that representative's team. Council representatives should bring in moderation/mediation resources as needed to facilitate those conversations. Moderation can help resolve the issue, and/or determine if the issue is actionable and motivates some level of escalation.

While it is out of scope for this RFC to specify how individual teams ensure their representatives are held accountable, we encourage teams to use the above mechanisms as inspiration for their own policies and procedures.

## 確保能追究團隊之責任

Teams regularly coordinate and cooperate with each other, and have conversations about their needs; under normal circumstances the Council must respect the autonomy of individual teams.

However, the Council serves as a means for teams to jointly hold each other accountable, to one another and to the Project as a whole. The Council can:

- Ask a team to reconsider a decision that failed to take the considerations of other teams or the Project as a whole into consideration.
- Encourage teams to establish processes that more regularly take other teams into consideration.
- Ensure a shared understanding of teams' purviews.
- Ensure teams are willing and able to fulfill those purviews.
- Establish new teams that split a team's purview up into more manageable chunks.

The accountability process must not be punitive, and the process must be done with the active collaboration of the teams in question.

In extreme circumstances where teams are willfully choosing to not act in good faith with regards to the wider Project, the Council has the authority to change a team's purview, move some subset of a team's purview to another team, or remove a team entirely. This is done through the Council's regular decision making process. (This does not apply to the moderation team; see the next section for accountability between the Council and moderation team.)

# 審核、分歧與衝突

This section describes the roles of the Leadership Council and the moderation team in helping resolve disagreements and conflicts, as well as the interactions between those teams.

Disagreements and conflicts fall on a spectrum of interpersonal interaction. Disagreements are more factual and/or technical misalignments, while conflicts are more social or relational roadblocks to collaboration. Many interactions might display aspects of both disagreement and conflict. The Council can help with aspects of disagreement, while aspects of conflict are the purview of the moderation team.

This RFC does not specify moderation policy in general, only the portion of it necessary to specify interactions with the Council and the checks and balances between the Council and the moderation team. General moderation policy is out of scope for this RFC.

Much of the work of the Rust Project involves collaboration with other people, all of whom care deeply about their work. It's normal for people to disagree, and to feel strongly about that disagreement. Disagreement can also be a powerful tool for surfacing and addressing issues, and ideally, people who disagree can collaboratively and (mostly) amicably explore those disagreements without escalating into interpersonal conflicts.

Situations where disagreements and conflicts arise may be complex. Disagreements can escalate into conflicts, and conflicts can de-escalate into disagreements. If the distinction between a disagreement and a conflict is not clear in the situation, or if participants disagree, assume the situation is a conflict.

In the event of a conflict, involved parties should reach out to the moderation team to help resolve the conflict as soon as possible. Time is a critical resource in attempting to resolve a conflict before it gets worse or causes more harm.

## 團隊間之分歧

Where possible, teams should attempt to resolve disagreements on their own, with assistance from the Council as needed. The Council can make judgment calls to settle disagreements, but teams need to maintain good working relationships with each other to avoid persistent disagreements or escalations into conflicts.

Potential resolution paths for disagreements between teams could include selecting a previously discussed option, devising a new option, deciding whose purview the decision falls in, or deciding that the decision is outside the purviews of both teams and leaving it to the Council to find a new home for that work.

## 涉及團隊或專案成員之衝突

Conflicts involving teams or Project members should be brought to the moderation team as soon as possible. The Council can help mitigate the impact of those conflicts on pending/urgent decisions, but the moderation team is responsible for helping with conflicts and interpersonal issues, across teams or otherwise.

Individuals or teams may also voluntarily engage in other processes to address conflicts or interpersonal issues, such as non-binding external mediation. Individuals or teams should keep the moderation team in the loop when doing so, and should seek guidance from the moderation team regarding appropriate resources or approaches for doing so. Individuals or teams must not use resources that would produce a conflict of interest.

## 審核人代表團

The moderation team must at all times maintain a publicly documented list of "contingent moderators", who must be approved by both the moderation team and the Council via internal consent decision. The moderation team and contingent moderation team should both consist of at least three members each. The contingent moderators must be:
- Not part of the current moderation team *or* the Leadership Council.
- Widely trusted by Rust Project members as jointly determined by the Council and moderation team; this will often mean they're already part of the Project in some capacity.
- Qualified to do moderation work and [audits] as jointly determined by the Council and moderation team. More detailed criteria and guidelines will be established by moderation policy, which is out of scope for this RFC.
- Willing to serve as contingent moderators: willing to do audits, and willing to do interim moderation work if the moderation team dissolves or becomes unavailable, until they can appoint new full moderators. (The contingent moderators are not expected to be willing to do moderation work long-term.)
- Willing to stay familiar with moderation policy and procedure to the standards expected of a moderation team member (including any associated training). Contingent moderators should receive the same opportunities for training as the moderation team where possible.

The need for contingent moderators arises in a high-tension situation, and the Project and Council must be prepared to trust them to step into that situation. Choosing people known and trusted by the rest of the Project helps lower tensions in that situation.

Moderation is a high-burnout activity, and individual moderators or the moderation team may find itself wishing to step away from that work. Note that one or more individual moderators may always choose to step down, in which case the moderation team should identify and bring in new moderators to fill any gaps or shortfalls; if the moderation team asks a contingent moderator to become a full moderator, the team should then appoint a new contingent moderator. An individual moderator who stepped down *may* be selected as a contingent moderator. If the moderation team as a whole becomes simultaneously unavailable (as determined jointly by the Council and contingent moderators via internal consent decision), or chooses to step down simultaneously, the contingent moderators become the interim moderation team and must promptly appoint new contingent moderators and start seeking new full moderators.

As the contingent moderator role does not have any regular required activities outside of exceptional situations, those appointed to that role must have regular check-ins with the moderation team, to reconfirm that they're still willing to serve in that role, and to avoid a circumstance in which the contingent moderators are abruptly needed and turn out to be unavailable.

## 審核團隊之政策與程序

The moderation team has a duty to have robust policies and procedures in place. The Council provides oversight and assistance to ensure that the moderation team has those policies and procedures and that they are sufficiently robust.

The Council may provide feedback to the moderation team and the moderation team is required to consider all feedback received. If the Council feels the moderation team has not followed moderation policies and procedures, the Council may [require an audit][audits] by the contingent moderators. However, the Council may not overrule a moderation decision or policy.

## 稽核
[audits]: #audits

If any Council member believes a moderation decision (or series of decisions) has not followed the moderation team's policies and procedures, they should promptly inform the moderation team. The Council and moderation team should then engage with each other, discuss and understand these concerns, and work to address them.

One of the mechanisms this RFC provides for checking the moderation team's actions in a privacy-preserving manner is an audit mechanism. In any case where any Council member believes moderation team actions have not followed documented policies or procedures, the Council member may decide to initiate the audit process. (In particular, they might do this in response to a report from a community member involved in a moderation situation.) This happens *in addition* to the above engagement and conversation; it is not a replacement for direct communication between the Council and the moderation team.

In an audit, the contingent moderation team works with the moderation team to establish whether the moderation team followed documented policies and procedures. This mechanism necessarily involves the contingent moderation team using their own judgment to evaluate moderation policy, specific evidence or communications, and corresponding moderation actions or proposed actions. However, this mechanism is not intended to second-guess the actions themselves; the audit mechanism focuses on establishing whether the moderation team is acting according to its established policy and procedures.

The contingent moderators also reach out to the Council to find out any additional context they might need.

Moderation processes and audits both take time, and must be performed with diligence. However, the Council, contingent moderators, and moderation team should all aim to communicate their concerns and expectations to each other in a reasonably timely fashion and maintain open lines of communication.

Contingent moderators must not take part in decisions or audits for which they have a conflict of interest. Contingent moderators must not have access to private information provided to moderation before the contingent moderator was publicly listed as part of the contingent moderation team; this gives people speaking with the moderation team the opportunity to evaluate potential concerns or conflicts of interest.

The discussions with the Council and the contingent moderation team may discover that the moderation team had to make an exception in policy for a particular case, as there was an unexpected condition in policies or that there was contextual information that couldn't be incorporated in policy. This is an expected scenario that merits additional scrutiny by the contingent moderation team on the rationale for making an exception and the process for deciding the necessity to make an exception, but is not inherently a violation of moderation team responsibilities.

As the audit process and the Council/moderation discussions proceed, the moderation team may decide to alter moderation policies and/or change the outcome of specific moderation decisions or proposed decisions. This is solely a decision for the moderation team to make.

The contingent moderation team must report the results of the audit to the moderation team and the Council for their review. This must not include any details that may reveal private information, either directly or indirectly. Together with the discussions with the moderation team, this should aim to address the concerns of the Council.

## 最終問責機制

The Leadership Council and moderation team each have substantial power within the Rust Project. This RFC provides many tools by which they can work out conflicts. This section outlines the last-resort mechanisms by which those teams can hold each other accountable. This section is written in the hopes that it will never be needed, and that teams will make every possible effort to resolve conflicts without reaching this point.

If the Council believes there is a systemic problem with the moderation team (whether based on an audit report from the contingent moderation team or otherwise), and the Council and moderation team cannot voluntarily come to agreement on how to address the situation, then as a **last resort**, the Council (by unanimous decision) may simultaneously dissolve itself and the moderation team. The top-level teams must then appoint new representatives to the Council, and the contingent moderation team becomes the new interim moderation team.

Conversely, if the moderation team believes the Council has a systemic problem, and the Council and moderation team cannot voluntarily come to agreement on how to address the situation, then as a **last resort**, the moderation team (by unanimous decision) may simultaneously dissolve itself and the Council. This process can only be enacted if there are at least three moderation team members. The top-level teams must then appoint new representatives to the Council, and the contingent moderation team becomes the new interim moderation team.

The moderation team's representative is recused from the decision to dissolve the Council and moderation team to avoid conflicts of interest, though that representative must still step down as well.

The removed representatives and moderators may not serve on either the Council or the moderation team for at least one year.

By default, the new Council and interim moderation team will take responsibility for clearly communicating the transition.

This mechanism is an absolute last resort. It will almost certainly produce suboptimal outcomes, to say the least. If situations escalate to this outcome, many things have gone *horribly* wrong, and those cleaning up the aftermath should endeavor to prevent it from ever happening again. The indication (by either the moderation team or the Council) that the situation *might* escalate to this point should be considered a strong signal to come to the table and find a way to do "Something Else which is Not That" to avoid the situation.

## 涉及專案成員之審核措施
[moderation-actions-involving-Project-members]: #moderation-actions-involving-Project-members

The moderation team, in the course of doing moderation work, necessarily requires the ability to take action not just against members of the Rust community but also against members of the Rust Project. Those actions may span the ladder of escalation all the way from a conversation to removal from the Project. This puts the moderation team in a position of power and trust. This RFC seeks to provide appropriate accountability and cross-checks for the moderation team, as well as for the Council.

If the moderation team plans to enact externally visible sanctions against any member of the Rust Project (anything that would create a conspicuous absence, such as removal from a role, or exclusion from participation in a Project space for more than a week), then any party may request that an [audit][audits] take place by reaching out to either the Council or contingent moderators, and that audit will be automatically granted.

For the first year after the ratification of this RFC, audits are automatically performed even without a request, to ensure the process is functional. After that time, the Council and moderation team will jointly review and decide whether to renew this provision.

When the moderation team sends a warning to a Project member, or sends a notification of moderation action regarding a Project member, that message will mention the option of requesting an audit.

Conflicts regarding Project members should be brought to the moderation team as soon as possible.

## 涉及理事會代表之衝突

Conflicts involving Council representatives, or alternates, follow the same process as conflicts involving Project members. The moderation team has the same ability to moderate representatives or alternates as any other member of the Project, including the required [audit][audits] by the contingent moderators for any externally visible sanction. This remains subject to the same accountability mechanisms as for other decisions of the moderation team.

In addition to the range of moderation actions already available, the moderation team may take the following additional actions for representatives or alternates as a near-last resort, as a lesser step on the ladder of escalation than removing a member from the Project entirely. These actions are not generally specific to the Council, and apply to other Rust teams as well.

- The moderation team may decide to remove a representative from the Council. The top-level team represented by that representative should delegate a new representative to serve the remainder of the term, starting immediately.
- The moderation team may decide to prevent a Project member from becoming a Council representative.
- The moderation team and Council (excluding the affected parties) may jointly decide (as a private operational consent decision) to apply other sanctions limiting the representative's involvement in the Council. (In this scenario, representatives are not excluded if they have a conflict of interest, as the entire Council will have to cooperate to make the sanctions effective. If the conflicts of interest thus prevent applying these partial sanctions, the moderation team always has the option of full sanctions such as removal.)

All of these also trigger a required audit. The Council must also be notified of any moderation actions involving representatives or alternates, or actions directly preventing people from becoming representatives.

## 涉及審核團隊成員之衝突

Conflicts involving a member of the moderation team will be handled by the remaining members of the moderation team (minus any with a conflict of interest), *together with* the contingent moderation team to provide additional oversight. Any member of the moderation or contingent moderation team should confer with the Council if there is a more systemic issue within the moderation team. The contingent moderators must audit this decision and must provide an audit report to the Council and moderation team.

# 本案之批准

自 2021 年 11 月以來，下列成員實質上已在專案擔任中領導角色：所有 Core 團隊成員、所有審核團隊成員、Rust Foundation 理事會（board）上的所有專案代表以及「一級」團隊的負責人：
- 編譯器
- Crates.io
- 開發工具
- 基礎架構
- 語言
- 函式庫
- 審核（已包含在上方）
- 發佈

此 RFC 將以標準 RFC 程序審批，由前述實質上的領導層成員來批准。這些成員還應代表專案中其他成員提出異議，更具體來說，團隊負責人應徵求他的團隊和子團隊的回饋。

# 附註

[^core]: Unlike in some other Open Source projects, the Rust Project's "core team" does not refer to a group that decides the technical direction of the Project. As explained in more detail elsewhere in the RFC, the Rust Project distributes decision-making to many different teams who have responsibility for their specific purview. For example, the compiler team is in charge of the Rust compiler, the language team is in charge of language evolution, etc. This is part of why this RFC discontinues use of the term "core team".

[^authority]: The term 'authority' here refers to the powers and responsibilities the Council has to ensure the success of the Rust Project. This RFC lays out the limits of these powers, so that the Council will delegate the authority it has to teams responsible for the concerns of the Project. These concerns may include - but are not limited to - product vision, day-to-day procedures, engineering decisions, mentoring, and marketing.

[^teams]: Throughout this document, "teams" includes subteams, working groups, project groups, initiatives, and all other forms of official collaboration structures within the Project. "Subteams" includes all forms of collaboration structures that report up through a team.

[^under-multiple-teams]: Subteams or individuals that fall under multiple top-level teams should not get disproportionate representation by having multiple representatives speaking for them on the Council. Whenever a "diamond" structure like this exists anywhere in the organization, the teams involved in that structure should strive to avoid ambiguity or diffusion of responsibility, and ensure people and teams know what paths they should use to raise issues and provide feedback.

[^bootstrapping-new-teams]: The Council consists only of the representatives provided to it by top-level teams, and cannot appoint new ad hoc members to itself. However, if the Council identifies a gap in the project, it can create a new top-level team. In particular, the Council can bootstrap the creation of a team to address a problem for which the Project doesn't currently have coordinated/organized expertise and for which the Council doesn't know the right solution structure to charter a team solving it. In that case, the Council could bring together a team whose purview is to explore the solution-space for that problem, determine the right solution, and to return to the Council with a proposal and charter. That team would then provide a representative to the Council, who can work with the Council on aspects of that problem and solution.

[^number-of-representatives]: This also effectively constrains the number of Council representatives to the same range. Note that this constraint is independently important.

[^representative-selection]: 最終整體來說，作為一位理事會代表是為了服務個別的團隊以及 Rust 計畫。儘管此 RFC 的作者希望這個職位能夠滿足並且吸引任何足以勝任這份工作的人，我們仍然希望它不被視為是用來爭奪地位的職位。

[^council-roles]: The Council is not required to assign such roles exclusively to Council representatives; the Council may appoint any willing Project member. Such roles do not constitute membership in the Council for purposes such as decision-making.
