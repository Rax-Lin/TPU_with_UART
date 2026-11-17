# TPU with UART

A 4 × 4 output-stationary systolic array for FP32 matrix multiplication on the Nexys A7-100T. Python sends matrices over UART and verifies the FPGA result.

## Requirements

- Nexys A7-100T, Vivado 2024.1, Python 3 and pySerial

## Usage

1. Open `UART_TPU/UART_TPU.xpr` in Vivado, generate any required IP products and program the board with the generated bitstream.
2. Connect the board's UART over USB and run:

   ```powershell
   python -m pip install -r requirements.txt
   python uart_test.py --port COM5 --seed 42 --min-dim 4 --max-dim 4
   ```

3. Replace `COM5` with the board's serial port. When prompted, press BTNC, then press Enter. The script reports the verification result.

UART uses 115200 baud, 8 data bits, no parity and one stop bit. Run `python uart_test.py --help` for more options.

## Files

- `uart_test.py` — host test and verification.
- `UART_TPU/UART_TPU.srcs/` — hardware sources, IP, constraints and testbench.

The existing implementation log reports an unmatched `LED[5]` constraint. A clean Vivado rebuild and hardware test remain to be verified.