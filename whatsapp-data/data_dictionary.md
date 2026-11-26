# Data Dictionary and Feature Descriptions

This document outlines the schema, column definitions, data types, and visual analysis mappings for all datasets in `whatsapp-data/`.

---

## 1. Message-Level Feature Matrix (`wa_messages.csv`)

| Column Name | Data Type | Description | Example |
|---|---|---|---|
| `msg_id` | Integer | Unique incremental identifier for each message across all chats | `1042` |
| `chat_id` | String | Anonymized chat identifier (`c001`, `c002`, ...) | `c042` |
| `chat_type` | String | Chat structure: `direct` ($\le 2$ participants) or `group` ($\ge 3$ participants) | `direct` |
| `num_participants` | Integer | Count of unique active participants in the chat | `2` |
| `sender_role` | String | Role of the message sender: `self` or `other` | `self` |
| `sender_id` | String | Intra-chat sender pseudonym (`self`, `u01`, `u02`, ...) | `self` |
| `timestamp` | Timestamp | Message timestamp in local time (Europe/Istanbul, minute precision) | `2025-03-14 15:42:00` |
| `date` | Date | Calendar date (`YYYY-MM-DD`) | `2025-03-14` |
| `hour` | Integer | Hour of the day (`0-23`) | `15` |
| `minute` | Integer | Minute of the hour (`0-59`) | `42` |
| `day_of_week` | Integer | Day of week (`0 = Monday, ..., 6 = Sunday`) | `4` |
| `month` | Integer | Month of the year (`1-12`) | `3` |
| `year` | Integer | Year | `2025` |
| `is_weekend` | Binary (`0/1`) | Weekend flag (`1` for Saturday/Sunday, `0` for weekdays) | `0` |
| `char_count` | Integer | Character length of the message body (0 for media/deleted placeholders) | `48` |
| `word_count` | Integer | Word count of the message body | `8` |
| `line_count` | Integer | Number of lines in the message | `1` |
| `emoji_count` | Integer | Count of Unicode emoji symbols | `2` |
| `exclamation_count`| Integer | Count of exclamation marks (`!`) | `1` |
| `question_count` | Integer | Count of question marks (`?`) | `0` |
| `uppercase_ratio` | Float | Ratio of uppercase letters to total alphabet characters (`0.0 - 1.0`) | `0.0526` |
| `has_url` | Binary (`0/1`) | URL/web link indicator | `0` |
| `is_media` | Binary (`0/1`) | Media attachment placeholder flag (photo, video, audio, sticker) | `0` |
| `is_deleted` | Binary (`0/1`) | Deleted message placeholder flag | `0` |
| `is_forwarded` | Binary (`0/1`) | Forwarded message flag | `0` |
| `is_paste_suspected`| Binary (`0/1`) | Paste/chain message indicator ($\ge 500$ chars, $\ge 5$ lines, URL, or duplicate body) | `0` |
| `prev_sender_role` | String | Sender role of the preceding message in the same chat (`self` / `other`) | `other` |
| `time_since_prev_msg_sec` | Float | Elapsed time in seconds from preceding message in the same chat | `45.0` |
| `session_id` | Integer | Conversation session sequence number ($\le 6$ hours gap remains same session) | `12` |
| `is_session_starter` | Binary (`0/1`) | Flag indicating whether this message starts a new session | `0` |
| `turn_id` | Integer | Conversational turn within session (consecutive messages by same role = 1 turn) | `3` |
| `response_delay_sec` | Float | Response latency (seconds since previous turn, populated on turn switches) | `45.0` |

---

## 2. Chat Summary Table (`wa_chat_summary.csv`)

| Column Name | Data Type | Description | Example |
|---|---|---|---|
| `chat_id` | String | Anonymized chat identifier (`c001`, `c002`, ...) | `c015` |
| `chat_type` | String | `direct` or `group` | `direct` |
| `num_participants` | Integer | Total unique senders in chat | `2` |
| `first_date` | Date | Date of first message | `2024-09-01` |
| `last_date` | Date | Date of last message | `2026-11-20` |
| `active_days_count` | Integer | Number of distinct active days with communication | `142` |
| `self_msg_count` | Integer | Total valid text messages sent by `self` | `850` |
| `other_msg_count` | Integer | Total valid text messages sent by `other` | `920` |
| `self_char_count` | Integer | Total characters sent by `self` | `24500` |
| `other_char_count` | Integer | Total characters sent by `other` | `26100` |
| `self_msg_share` | Float | Proportion of messages sent by `self` | `0.4802` |
| `session_count` | Integer | Total conversational sessions in chat | `65` |
| `self_session_starter_share` | Float | Proportion of sessions initiated by `self` | `0.5231` |
| `median_response_delay_self_sec` | Float | Median response delay of `self` in seconds | `120.0` |
| `median_response_delay_other_sec`| Float | Median response delay of `other` in seconds | `180.0` |

---

## 3. Daily Aggregate Time Series (`wa_daily.csv`)

| Column Name | Data Type | Description | Example |
|---|---|---|---|
| `date` | Date | Calendar date (`2024-08-05` to `2026-11-24`) | `2025-05-10` |
| `self_msg_count` | Integer | Total messages sent by `self` on this day | `35` |
| `self_char_count` | Integer | Total characters typed by `self` on this day | `1120` |
| `self_active_chat_count`| Integer | Number of distinct chats where `self` was active | `6` |
| `other_msg_count` | Integer | Total incoming messages received on this day | `42` |
| `other_char_count` | Integer | Total incoming characters received on this day | `1350` |
| `self_night_ratio` | Float | Ratio of `self` messages sent between 00:00 and 06:00 | `0.0571` |
| `self_first_msg_hour` | Float | Decimal hour of first message sent by `self` (e.g. 9.50 = 09:30) | `09.42` |
| `self_last_msg_hour` | Float | Decimal hour of last message sent by `self` | `23.15` |

---

## 4. Hourly Aggregate Matrix (`wa_hourly.csv`)

| Column Name | Data Type | Description | Example |
|---|---|---|---|
| `date` | Date | Calendar date | `2025-05-10` |
| `hour` | Integer | Hour bin (`0-23`) | `14` |
| `self_msg_count` | Integer | Messages sent by `self` during this hour | `5` |
| `self_char_count` | Integer | Characters typed by `self` during this hour | `165` |
| `other_msg_count` | Integer | Messages received during this hour | `8` |
| `other_char_count` | Integer | Characters received during this hour | `240` |
