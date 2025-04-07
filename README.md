# Stock Trading với TD3 (Twin Delayed DDPG)

Dự án này sử dụng thuật toán học tăng cường TD3 (Twin Delayed Deep Deterministic Policy Gradient) để tối ưu hóa lợi nhuận đầu tư cổ phiếu. Mô hình được huấn luyện với dữ liệu lịch sử của cổ phiếu AMAT.

## Tổng quan

Project này xây dựng một agent sử dụng TD3 để học cách tối ưu hóa chiến lược giao dịch cổ phiếu trong môi trường giao dịch tùy chỉnh. Agent này có thể quyết định khi nào mua, bán, hoặc giữ cổ phiếu dựa trên dữ liệu thị trường hiện tại và trạng thái danh mục đầu tư.

## Tính năng

- **Môi trường giao dịch cổ phiếu tùy chỉnh (StockEnv)** với các quy tắc giao dịch thực tế
- **Thuật toán TD3** được tối ưu hóa cho giao dịch cổ phiếu
- **Replay Buffer** để cải thiện hiệu quả học tập
- **Hiển thị và phân tích** kết quả chi tiết

## Các tham số và quy tắc giao dịch

- **Vốn khởi điểm:** 100,000 USD
- **Quy tắc mua:** Mỗi giao dịch mua trong khoảng 44% đến 57% số tiền mặt hiện có
- **Quy tắc bán:** Mỗi giao dịch bán trong khoảng 35% đến 84% số cổ phiếu đang nắm giữ
- **Phí giao dịch:** 0.5% giá trị giao dịch
- **Phạt không giao dịch:** 150 USD sau 10 phiên không giao dịch
- **Điều kiện thua:**
  - Tổng tài sản < 50,000 USD
  - Tiền mặt <= -5,000 USD
- **Điều kiện thắng:** Tổng tài sản đạt 1,000,000 USD

## Cấu trúc dự án

```
stock_trading_td3/
├── data/
│   ├── AMAT_historical_data_train.csv
│   └── AMAT_historical_data_test.csv
├── models/
│   └── td3.py                  # Mã nguồn của thuật toán TD3
├── utils/
│   ├── stock_env.py            # Môi trường giao dịch cổ phiếu
│   ├── visualization.py        # Công cụ hiển thị kết quả
│   └── helpers.py              # Các hàm trợ giúp
├── results/                    # Thư mục lưu kết quả và mô hình
├── main.py                     # Chương trình chính
├── requirements.txt            # Các thư viện cần thiết
└── README.md                   # Tài liệu dự án
```

## Cài đặt

1. Clone repository này:
```bash
git clone https://github.com/username/stock_trading_td3.git
cd stock_trading_td3
```

2. Cài đặt các thư viện cần thiết:
```bash
pip install -r requirements.txt
```

3. Chuẩn bị dữ liệu:
   - Đặt tệp `AMAT_historical_data_train.csv` và `AMAT_historical_data_test.csv` vào thư mục `data/`

## Cách sử dụng

### Huấn luyện mô hình

```bash
python main.py --mode train
```

### Đánh giá mô hình

```bash
python main.py --mode evaluate --model_path results/best_model
```

### Giao dịch trực tiếp

```bash
python main.py --mode trade --model_path results/best_model
```

## Thuật toán TD3

TD3 (Twin Delayed Deep Deterministic Policy Gradient) là phiên bản cải tiến của DDPG với 3 kỹ thuật chính:
1. **Twin Critic Networks:** Sử dụng 2 mạng Critic để giảm thiểu overestimation bias
2. **Delayed Policy Updates:** Cập nhật mạng Actor ít thường xuyên hơn Critic
3. **Target Policy Smoothing:** Thêm nhiễu vào các hành động dự đoán để tăng độ ổn định

## Kết quả

Mô hình được đánh giá dựa trên:
- Tổng tài sản cuối cùng
- Tỉ lệ lợi nhuận (ROI)
- Sharpe ratio
- Drawdown tối đa

## Tác giả

- [Your Name](https://github.com/Datphi-AI)

## Tài liệu tham khảo

- [Twin Delayed Deep Deterministic Policy Gradient (TD3)](https://arxiv.org/abs/1802.09477)
- [Reinforcement Learning in Stock Trading](https://arxiv.org/abs/1805.09318)
