# prompt存档

# 网站SEO审核Prompt



Audit this Shopify ecommerce webpage and create a downloadable, self\-contained HTML report with original page screenshots, numbered markup and actionable comments\.



Use the supplied materials and verified public sources\. Proceed with reasonable assumptions when optional context is missing, and state those assumptions\.

SCOPE

Audit the specified page in depth\. Inspect directly relevant linked pages only where necessary to verify pricing, software requirements, package contents, policies or inconsistencies\. Do not turn this into an unrestricted full\-site audit\.



Cover five areas:

1. SEO

- Page title, meta description, H1 and heading structure\.

- Clear product\-category terminology and alignment with buyer search intent\.

- Canonical URL, indexability signals and relevant internal links\.

- Informative image alt text\.

- Product structured data and consistency with visible pricing, availability and product information\.

- Relevant crawlability, localization and performance issues that can actually be verified\.

2. GEO: visibility and accurate representation in AI\-generated answers

- Whether the page clearly explains what the product is, who it is for and how it works\.

- Whether important product facts are understandable without additional context\.

- Clear relationships between hardware, software, accessories and subscriptions\.

- Useful specifications, FAQs, compatibility information and purchasing requirements\.

- Evidence supporting numerical claims and major benefits\.

- Consistency between visible content, metadata, structured data and linked pages\.

Focus on accurate, useful content for people and search systems\. Do not promise rankings, AI citations or percentage improvements\. Do not treat special AI files or FAQ schema as mandatory for AI visibility\.

3. Copywriting: 

Include:

- Incorrect grammar that materially affects meaning or professionalism\.

- Wrong product names, mistranslations or factual contradictions\.

- Misleading claims or missing qualifications\.

- Unclear price units, minimum quantities, included items, required accessories, subscriptions or renewal terms\.

- Copy that could cause buyers to misunderstand the product or purchase\.

- US/UK spelling inconsistencies\.

Exclude:

- Rewriting clear copy simply to make it sound different\.

- Treating acceptable headline shorthand as a serious grammatical error\.

If no serious copy errors are found, say so\. Do not invent issues to fill this section\.

4. Design, attractiveness and usability

Assess the actual rendered page:

- First\-screen clarity and product presentation\.

- Visual hierarchy and purchase\-button prominence\.

- Image quality, cropping, realism and relevance\.

- Consistent spacing, alignment, typography, colors and image treatment\.

- Excessive repetition, empty space or difficult\-to\-scan sections\.

- Distracting overlays, obstructed controls, horizontal scrolling and responsive problems\.

Separate objective usability defects from subjective design recommendations\. Explain what the buyer sees and why it matters\. Do not describe a legitimate payment\-provider brand color as a defect by itself\.

5. Inconsistencies

Check for material differences in:

- Product names and specifications\.

- Pricing, package contents and software terms\.

- Claims and their qualifiers\.

- Button labels and destinations\.

- Navigation, policies and support information\.

- Localized product names and meaning\.

- Visual patterns within the page\.

EVIDENCE AND ACCURACY RULES

- Inspect before judging\. Do not produce a generic checklist presented as findings\.

- Distinguish the attached snapshot from the current live page\. Identify differences and record the audit date\.

- Label each item as:

A\. Confirmed issue

B\. Needs verification

C\. Design recommendation

- Quote exact original wording or show the exact affected area\.

- Do not call a page broken, unavailable or non\-indexed merely because your browsing tool fails or a search returns no result\.

- Do not claim missing structured data based only on a text extraction\. Inspect rendered HTML or label the check unverified\.

- Do not claim mobile, Safari or other browser testing unless you actually performed it\. Record browser and viewport for reproduced layout bugs, and do not generalize one browser’s behavior to all visitors\.

- Do not infer poor Core Web Vitals from page length or image count\. Distinguish implementation risks from measured performance\.

- Do not invent search volumes, customer reviews, validation studies, product capabilities or commercial terms\.

- Missing visible proof does not mean a product claim is false: label it “proof not shown” and request the supporting evidence\.

- Preserve valid existing implementations\. Do not recommend changing established URLs merely for cosmetic keyword improvements; explain any real benefit and migration risk\.

- Check current authoritative documentation for technical recommendations\. Include concise source links where relevant\.

- Do not assign arbitrary numerical SEO/GEO scores\.

- Do not submit forms, add items to carts, place orders or edit the live store\.

If page access or tools are limited, continue with the supplied files where possible and clearly list what could not be checked\. Never recreate an unseen page and label it “original\.”

HTML REPORT REQUIREMENTS

Create an actual downloadable \.html file, not only HTML code in the chat\.

Include:

1. Executive summary

- Overall assessment\.

- The five most important issues, or fewer if fewer are supported\.

- What already works and should be preserved\.

- Scope, sources and testing limitations\.

2. Annotated original page

- Use real screenshots of the supplied or live page\.

- Add numbered pins, boxes or highlights directly over the relevant areas\.

- Match each annotation to a nearby comment\.

- Keep original screenshots unaltered apart from clearly identified markup\.

- For metadata or code issues not visible in screenshots, show exact extracted evidence in a separate panel\.

3. Detailed findings

For each unique issue, show:

- Issue ID\.

- Category tags\.

- Evidence status\.

- Priority\.

- Page location\.

- Original wording, screenshot or technical evidence\.

- Clear explanation in plain language\.

- Specific correction\.

- Replacement wording where appropriate\.

- Suggested owner: Copywriting/PMM, Design, Frontend or Ecommerce\.

- Acceptance criteria for checking the fix\.

Avoid duplicating the same issue in several sections\. Use multiple category tags instead\.

4. Prioritized action list

- Priority 1: significant purchasing barriers, misleading information, major broken functionality or verified indexing blockers\.

- Priority 2: meaningful search, clarity, trust or usability improvements\.

- Priority 3: lower\-impact polish and optional enhancements\.

Do not classify cosmetic changes or minor layout differences as launch blockers\.

5. Verification checklist

List remaining checks that require product\-owner confirmation, browser testing, Search Console, analytics, Merchant Center or performance tools\.

PRESENTATION AND QUALITY CONTROL

- Make the report professional, easy to scan and useful for assigning tasks\.

- Use readable typography, clear category labels and responsive layouts\.

- Include original vs recommended copy side by side\.

- Embed screenshots and CSS where possible so the file can be opened without missing assets\.

- Keep reporting functionality separate from the original storefront: no active checkout forms or tracking scripts\.

- Verify that images load, annotations align, links and navigation work, and text is readable\.

- If visual preview is unavailable, say so and describe the validation actually completed\.

- Final response: provide the HTML download link and a short summary of the main findings\.

Prioritize evidence and useful corrections over report length or number of issues\.

