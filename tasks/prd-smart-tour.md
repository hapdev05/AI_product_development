# PRD: SmartTour

## 1. Introduction / Overview

### 1.1 Product name

**SmartTour**

### 1.2 Product description

SmartTour là ứng dụng mobile hỗ trợ người dùng tự động xây dựng lịch trình du lịch tại Đà Nẵng dựa trên thời gian chuyến đi, sở thích của người dùng, địa điểm du lịch và đặc biệt là dữ liệu dự báo thời tiết.

Thay vì người dùng phải tự tìm địa điểm, xem dự báo thời tiết và sắp xếp lịch trình thủ công, SmartTour tổng hợp các thông tin này để đề xuất một lịch trình theo từng ngày và từng khung giờ.

Ứng dụng được định hướng phát triển bằng **React Native** cho mobile. Dữ liệu thời tiết được lấy từ Weather API phù hợp. Thành phần AI/thuật toán lập lịch có thể được tích hợp ở lớp backend hoặc service riêng.

### 1.3 Problem

Việc tự lập kế hoạch du lịch thường yêu cầu người dùng:

- Tìm kiếm nhiều địa điểm khác nhau.
- Kiểm tra thời gian hoạt động của địa điểm.
- Xem dự báo thời tiết cho từng ngày.
- Tự sắp xếp các địa điểm theo thời gian.
- Tự điều chỉnh kế hoạch khi thời tiết thay đổi.
- Ước lượng thời gian di chuyển giữa các địa điểm.

Đặc biệt với chuyến đi ngắn ngày tại Đà Nẵng, một lịch trình không phù hợp với thời tiết có thể khiến người dùng phải thay đổi kế hoạch.

SmartTour giải quyết vấn đề này bằng cách đưa dữ liệu thời tiết vào quá trình lập lịch trình.

---

## 2. Goals

### 2.1 Product goals

- Cho phép người dùng tạo một chuyến du lịch Đà Nẵng bằng các thông tin cơ bản.
- Tự động đề xuất lịch trình theo từng ngày.
- Sử dụng dữ liệu dự báo thời tiết làm một trong các yếu tố chính khi lập lịch.
- Đề xuất hoạt động phù hợp với điều kiện thời tiết.
- Cho phép người dùng xem chi tiết từng ngày và từng hoạt động.
- Cho phép người dùng chỉnh sửa hoặc tạo lại lịch trình.
- Có giao diện mobile rõ ràng, dễ sử dụng.
- Tạo codebase React Native có cấu trúc rõ ràng để nhóm tiếp tục phát triển.

### 2.2 MVP goals

Phiên bản MVP tập trung vào luồng:

**Nhập thông tin chuyến đi → lấy dữ liệu thời tiết → phân tích điều kiện → tạo lịch trình → hiển thị lịch trình.**

---

## 3. Target Users

### Primary user

Khách du lịch đến Đà Nẵng muốn nhanh chóng có một lịch trình phù hợp với thời gian và thời tiết.

### Example user

Một người dùng muốn đi Đà Nẵng 3 ngày và nhập:

- Điểm đến: Đà Nẵng
- Ngày bắt đầu: 10/10
- Ngày kết thúc: 12/10
- Sở thích: biển, tham quan, ăn uống
- Cường độ: vừa phải

SmartTour lấy dự báo thời tiết và tạo lịch trình cho 3 ngày.

---

## 4. User Stories

### US-001: Nhập thông tin chuyến đi

**Description:** As a traveler, I want to enter my trip information so that SmartTour can create a suitable itinerary.

**Acceptance Criteria:**

- [ ] Người dùng có thể nhập ngày bắt đầu chuyến đi.
- [ ] Người dùng có thể nhập ngày kết thúc chuyến đi.
- [ ] Người dùng có thể chọn các nhóm sở thích du lịch.
- [ ] Người dùng có thể chọn mức độ hoạt động mong muốn.
- [ ] Hệ thống kiểm tra ngày kết thúc không trước ngày bắt đầu.
- [ ] Không cho phép tiếp tục nếu các trường bắt buộc chưa hợp lệ.
- [ ] UI hiển thị thông báo lỗi rõ ràng khi dữ liệu không hợp lệ.
- [ ] Typecheck/lint passes.
- [ ] Verify in browser/device using appropriate frontend verification workflow.

### US-002: Lấy dữ liệu dự báo thời tiết

**Description:** As a traveler, I want SmartTour to retrieve weather information for my trip dates so that the itinerary can consider weather conditions.

**Acceptance Criteria:**

- [ ] Hệ thống xác định Đà Nẵng là địa điểm cần lấy dữ liệu thời tiết cho MVP.
- [ ] Hệ thống gọi Weather API thông qua lớp service phù hợp.
- [ ] Dữ liệu thời tiết được chuẩn hóa thành dữ liệu mà hệ thống lập lịch có thể sử dụng.
- [ ] Có trạng thái loading khi đang lấy dữ liệu.
- [ ] Có thông báo lỗi nếu Weather API không phản hồi hoặc trả về dữ liệu không hợp lệ.
- [ ] Không để API key của Weather API trong source code phía client.
- [ ] Typecheck/lint passes.

### US-003: Phân loại điều kiện thời tiết

**Description:** As a traveler, I want weather conditions to be interpreted so that activities can be selected appropriately.

**Acceptance Criteria:**

- [ ] Hệ thống có thể phân loại điều kiện thời tiết thành các nhóm tối thiểu: thuận lợi ngoài trời, có mưa/khả năng mưa, và điều kiện cần hạn chế hoạt động ngoài trời.
- [ ] Mỗi nhóm thời tiết có quy tắc lựa chọn hoạt động tương ứng.
- [ ] Quy tắc có thể được thay đổi mà không phải sửa nhiều phần UI.
- [ ] Nếu dữ liệu thời tiết thiếu, hệ thống sử dụng trạng thái không xác định và không tạo kết luận thời tiết giả.
- [ ] Typecheck/lint passes.

### US-004: Tạo lịch trình tự động

**Description:** As a traveler, I want SmartTour to automatically generate an itinerary so that I do not have to arrange activities manually.

**Acceptance Criteria:**

- [ ] Người dùng có thể bấm nút tạo lịch trình sau khi nhập đủ thông tin.
- [ ] Hệ thống tạo lịch trình theo từng ngày của chuyến đi.
- [ ] Mỗi ngày có danh sách hoạt động theo khung thời gian.
- [ ] Lịch trình sử dụng sở thích người dùng làm một yếu tố lựa chọn.
- [ ] Lịch trình sử dụng điều kiện thời tiết làm một yếu tố lựa chọn.
- [ ] Hoạt động ngoài trời được ưu tiên khi điều kiện phù hợp.
- [ ] Khi có mưa hoặc điều kiện không thuận lợi, hệ thống có thể ưu tiên hoạt động trong nhà hoặc hoạt động ít phụ thuộc thời tiết.
- [ ] Không tạo hai hoạt động trùng cùng một khung giờ.
- [ ] UI hiển thị trạng thái đang tạo lịch trình.
- [ ] Có thông báo rõ ràng nếu không thể tạo lịch trình.
- [ ] Typecheck/lint passes.
- [ ] Verify in browser/device using appropriate frontend verification workflow.

### US-005: Xem lịch trình theo ngày

**Description:** As a traveler, I want to view my itinerary day by day so that I can understand what to do during the trip.

**Acceptance Criteria:**

- [ ] Lịch trình được chia theo Day 1, Day 2, ... tương ứng với chuyến đi.
- [ ] Mỗi ngày hiển thị ngày tháng và thông tin thời tiết liên quan.
- [ ] Mỗi hoạt động hiển thị ít nhất tên, thời gian và địa điểm.
- [ ] Người dùng có thể mở chi tiết hoạt động.
- [ ] Người dùng có thể cuộn toàn bộ lịch trình.
- [ ] UI không hiển thị dữ liệu bị tràn hoặc chồng lấn trên kích thước màn hình mục tiêu.
- [ ] Typecheck/lint passes.
- [ ] Verify in browser/device using appropriate frontend verification workflow.

### US-006: Xem chi tiết địa điểm

**Description:** As a traveler, I want to see details about an activity location so that I can decide whether to follow the suggested itinerary.

**Acceptance Criteria:**

- [ ] Người dùng có thể mở chi tiết từ một activity trong itinerary.
- [ ] Chi tiết có tên địa điểm.
- [ ] Chi tiết có mô tả ngắn.
- [ ] Chi tiết có loại hoạt động.
- [ ] Chi tiết có thông tin liên quan đến điều kiện thời tiết nếu có.
- [ ] Có nút quay lại lịch trình.

### US-007: Tạo lại lịch trình

**Description:** As a traveler, I want to regenerate my itinerary so that I can receive another arrangement when the first plan is not suitable.

**Acceptance Criteria:**

- [ ] Người dùng có thể chọn tạo lại lịch trình.
- [ ] Hệ thống giữ lại thông tin chuyến đi đã nhập.
- [ ] Hệ thống tạo phương án mới dựa trên cùng các ràng buộc.
- [ ] Lịch trình cũ không bị thay đổi trước khi lịch trình mới được tạo thành công.
- [ ] Có trạng thái loading trong quá trình tạo lại.
- [ ] Typecheck/lint passes.
- [ ] Verify in browser/device using appropriate frontend verification workflow.

### US-008: Chỉnh sửa thông tin chuyến đi

**Description:** As a traveler, I want to edit my trip information so that I can update the itinerary when my plan changes.

**Acceptance Criteria:**

- [ ] Người dùng có thể quay lại màn hình thông tin chuyến đi.
- [ ] Các thông tin hiện tại được hiển thị.
- [ ] Người dùng có thể thay đổi ngày hoặc sở thích.
- [ ] Hệ thống kiểm tra dữ liệu mới.
- [ ] Người dùng có thể tạo lại lịch trình dựa trên thông tin mới.

### US-009: Xử lý lỗi và trạng thái rỗng

**Description:** As a traveler, I want clear error and empty states so that I understand what to do when data is unavailable.

**Acceptance Criteria:**

- [ ] Có loading state khi gọi API.
- [ ] Có error state khi API thất bại.
- [ ] Có empty state khi không có địa điểm phù hợp.
- [ ] Người dùng có thể thử lại khi request thất bại.
- [ ] Thông báo không tiết lộ API key hoặc thông tin kỹ thuật nhạy cảm.
- [ ] Typecheck/lint passes.

---

## 5. Functional Requirements

### Trip input

- **FR-1:** The system must allow users to enter a trip start date.
- **FR-2:** The system must allow users to enter a trip end date.
- **FR-3:** The system must validate that the end date is not earlier than the start date.
- **FR-4:** The system must allow users to select travel interests.
- **FR-5:** The system must allow users to select a preferred activity intensity.

### Weather

- **FR-6:** The system must retrieve weather data for Da Nang for the relevant trip dates.
- **FR-7:** Weather API credentials must not be hard-coded in the mobile client.
- **FR-8:** The system must normalize weather API data into an internal weather model.
- **FR-9:** The system must expose weather loading, success, and error states.
- **FR-10:** The system must use weather conditions as an input to itinerary generation.

### Itinerary generation

- **FR-11:** The system must generate an itinerary for every day in the selected trip period.
- **FR-12:** Each itinerary day must contain ordered activities.
- **FR-13:** Each activity must have a name, location, and time slot.
- **FR-14:** The system must avoid assigning two activities to the same time slot.
- **FR-15:** The system must consider user interests when selecting activities.
- **FR-16:** The system must consider weather conditions when selecting activities.
- **FR-17:** The system should prefer outdoor activities under suitable weather conditions.
- **FR-18:** The system should prefer indoor or weather-tolerant activities when rain or unsuitable weather is detected.
- **FR-19:** The system must show an explanation or weather context for weather-sensitive recommendations where practical.
- **FR-20:** The system must allow the user to regenerate the itinerary.

### Itinerary display

- **FR-21:** The system must display the itinerary grouped by day.
- **FR-22:** The system must display the weather associated with each day.
- **FR-23:** The system must display activity time and location.
- **FR-24:** The system must allow users to open activity details.
- **FR-25:** The system must provide clear loading, error, and empty states.

### Data and architecture

- **FR-26:** The React Native client must separate UI components from API/service logic.
- **FR-27:** Weather API calls must be isolated in a reusable service/module.
- **FR-28:** Itinerary data must use a consistent internal data model.
- **FR-29:** Environment-specific configuration must be separated from source code where applicable.
- **FR-30:** The project must provide setup instructions in the repository README.

---

## 6. Non-Goals / Out of Scope

The following items are outside the initial MVP unless the team explicitly expands the scope:

- Real-time flight booking.
- Hotel booking and payment.
- Restaurant reservation.
- Online payment.
- Tour guide booking.
- Full navigation/turn-by-turn GPS.
- Guaranteed real-world travel time calculations.
- Weather forecasts beyond what the selected Weather API reliably provides.
- Automatic booking of tickets or attractions.
- Social network features.
- Public sharing/feed of itineraries.
- Full multilingual localization.
- Complex loyalty/reward systems.
- Building a custom weather forecasting model.
- Treating AI-generated itinerary information as guaranteed or authoritative.

---

## 7. Design Considerations

### 7.1 Mobile-first UI

The application is designed primarily for mobile devices.

### 7.2 Main screens

The initial application should include:

1. Splash / Welcome
2. Home
3. Create Trip
4. Select Interests
5. Generating Itinerary
6. Itinerary Overview
7. Daily Itinerary
8. Activity / Place Detail
9. Weather Detail
10. Settings / Basic Profile (if included in MVP)

### 7.3 UX principles

- Keep trip creation short and understandable.
- Use clear date selection.
- Use recognizable weather icons and labels.
- Make each itinerary day visually distinct.
- Make the current weather context visible without opening multiple screens.
- Show clear feedback during network requests.
- Avoid overly dense screens.

### 7.4 Example itinerary

```text
SmartTour
Da Nang - 3 Days

DAY 1
Weather: Sunny

08:00 - My Khe Beach
10:30 - Son Tra Peninsula
12:00 - Lunch
14:00 - Linh Ung Pagoda
18:00 - Dinner
20:00 - Dragon Bridge
```

If rain is detected:

```text
DAY 2
Weather: Rain likely

09:00 - Museum / Indoor attraction
11:00 - Cafe
13:00 - Lunch
14:30 - Indoor entertainment
18:00 - Dinner
```

The exact places are examples only; actual recommendations must come from the application's place dataset/service.

---

## 8. Technical Considerations

### 8.1 Frontend

- React Native
- TypeScript
- React Navigation or an equivalent navigation solution
- A suitable state-management approach selected by the team
- Reusable UI components
- API/service layer separated from presentation

### 8.2 Backend

The project may use a backend API to:

- protect third-party API credentials,
- retrieve and normalize weather data,
- provide place data,
- generate and validate itinerary results,
- integrate an AI service if AI generation is used.

The exact backend framework is to be finalized by the team.

### 8.3 Weather API

The team must select a weather provider that supports the required forecast information.

The provider should support, where available:

- daily forecast,
- precipitation/rain information,
- temperature,
- weather condition,
- forecast date.

The application must handle API rate limits, failures, missing data, and changes in provider response format.

### 8.4 AI / itinerary engine

The initial implementation may use either:

1. rule-based itinerary generation,
2. an AI model,
3. or a hybrid approach.

A hybrid approach can use deterministic constraints for dates/time conflicts and AI or ranking logic for recommendations.

Regardless of implementation, generated output must be validated before being shown to the user.

### 8.5 Place data

Each place should have enough metadata for itinerary generation, such as:

- id
- name
- category
- indoor/outdoor classification
- suitable weather conditions
- recommended duration
- opening hours when available
- location
- user-interest tags

### 8.6 Security

- API keys must not be committed to Git.
- Secrets should be stored using environment configuration or a secure backend configuration.
- `.env` files containing secrets must be included in `.gitignore`.
- The repository must not contain production credentials.

### 8.7 Performance

- Weather data should not be requested repeatedly when the same valid data is already available.
- Loading states must be shown during network requests.
- Large lists should use appropriate React Native list components.
- The itinerary screen should remain responsive when displaying multiple days.

### 8.8 Error handling

The application must handle:

- no internet connection,
- Weather API failure,
- invalid user input,
- unavailable forecast data,
- itinerary generation failure,
- empty recommendation results.

---

## 9. Data Model Concept

The detailed ERD will be maintained separately, but the initial conceptual entities are:

```text
User
Trip
TripPreference
WeatherForecast
Place
Itinerary
ItineraryDay
ItineraryActivity
```

Possible relationships:

```text
User 1 ─── N Trip

Trip 1 ─── N ItineraryDay

ItineraryDay 1 ─── N ItineraryActivity

Place 1 ─── N ItineraryActivity

Trip 1 ─── N WeatherForecast
```

The final ERD may change during technical design.

---

## 10. Success Metrics

For the MVP, success is measured by whether the core flow can be completed successfully.

- A user can create a trip without application errors.
- Valid trip dates produce an itinerary containing all selected days.
- Weather information is displayed for available forecast dates.
- Generated activities reflect selected interests.
- Weather-sensitive activities change appropriately when weather conditions change.
- No itinerary contains overlapping activity time slots.
- Users can view the itinerary day by day.
- Users can regenerate an itinerary.
- The application handles network/API failure with a usable error state.
- The project can be cloned and started by another team member using the README instructions.
- The project passes the agreed lint/typecheck/build checks.

---

## 11. Acceptance Scenario

### Scenario A: Suitable weather

**Given** the user selects a 3-day Da Nang trip.

**When** the weather service reports suitable outdoor conditions for Day 1.

**Then** the generated itinerary may include outdoor destinations appropriate to the user's interests.

### Scenario B: Rain

**Given** the user selects a 3-day Da Nang trip.

**When** the weather service reports significant rain for Day 2.

**Then** the itinerary should reduce dependence on outdoor activities and may prioritize indoor or weather-tolerant activities.

### Scenario C: Invalid dates

**Given** the user enters a start date after the end date.

**When** the user attempts to generate an itinerary.

**Then** the application must prevent submission and show a validation message.

### Scenario D: Weather API unavailable

**Given** the user has entered a valid trip.

**When** the weather service cannot be reached.

**Then** the application must show an understandable error state and provide a retry action rather than displaying fabricated weather data.

---

## 12. Development Scope / Suggested Phases

### Phase 1 - Project setup

- Create React Native project.
- Configure TypeScript.
- Configure navigation.
- Establish folder structure.
- Add `.gitignore`.
- Add README.
- Add initial environment configuration example.

### Phase 2 - Trip creation UI

- Home screen.
- Create Trip screen.
- Date selection.
- Interest selection.
- Activity intensity selection.
- Validation.

### Phase 3 - Weather integration

- Weather service.
- Weather data model.
- Loading/error states.
- Weather display.

### Phase 4 - Place and itinerary engine

- Place dataset/API.
- Weather classification.
- Recommendation rules.
- Itinerary generation.
- Conflict validation.

### Phase 5 - Itinerary UI

- Daily itinerary.
- Activity cards.
- Place detail.
- Weather information.
- Regenerate itinerary.

### Phase 6 - Testing and refinement

- Unit tests for validation and itinerary rules.
- API error tests.
- UI verification.
- Typecheck/lint/build.
- README update.

---

## 13. Repository Structure

The expected project structure may start as:

```text
AI_product_development/
├── tasks/
│   └── prd-smart-tour.md
├── frontend/
│   └── smart-tour/
├── backend/
│   └── ...
├── docs/
│   └── erd/
├── README.md
└── .gitignore
```

The exact structure can be adjusted to match the team's existing repository architecture.

---

## 14. Non-Functional Requirements

### NFR-1: Usability

The core trip-generation flow should be understandable without technical knowledge.

### NFR-2: Reliability

The app must not crash because of a normal API/network failure.

### NFR-3: Security

Secrets and API credentials must not be committed to the public/shared source repository.

### NFR-4: Maintainability

Frontend UI, business logic, data models, and API services should be separated into understandable modules.

### NFR-5: Testability

Core itinerary rules and input validation should be implementable and testable independently of the UI.

### NFR-6: Portability

The project should be reproducible by team members following the repository setup instructions.

---

## 15. Open Questions

- Which Weather API provider will the team use?
- Which backend framework will be used?
- Which AI provider/model will be used, if AI is included?
- Will place data be manually curated, retrieved from an external API, or stored in the team's database?
- Will maps/navigation be included in the MVP or a later phase?
- Will user accounts and saved itineraries be included in the first release?
- What exact forecast horizon is required by the selected Weather API?
- How will itinerary quality be evaluated by the team?

---

## 16. Definition of Done

The SmartTour MVP is considered ready for the initial project milestone when:

- [ ] React Native project runs successfully.
- [ ] User can enter a valid Da Nang trip.
- [ ] Weather data can be retrieved and displayed.
- [ ] The system can generate a multi-day itinerary.
- [ ] Weather is used as an input to itinerary generation.
- [ ] User interests are used as an input to itinerary generation.
- [ ] Daily itinerary can be viewed.
- [ ] Activity details can be viewed.
- [ ] Regeneration is supported or explicitly scheduled for the next milestone.
- [ ] Network/API errors have usable error states.
- [ ] No secrets are committed to Git.
- [ ] Typecheck/lint/build passes.
- [ ] README contains setup instructions.
- [ ] The PRD and initial project codebase are committed to the team's Git repository.

