#include <iostream>
#include <vector>
#include <string>
//#define log(x) std::cout << x << std::endl;
//optimizing my bar graph code


class basic_utils {
public:
	static const int max(std::vector<int>& vecarray) {
		int max_val = 0;
		for (int i = 0; i < vecarray.size(); i++) {
			if (max_val < vecarray[i]) 
				max_val = vecarray[i];
		}
		return max_val;
	}
	static void process_data(std::vector<int>& processed,std::vector<int>& data) {
		for (int i = 0; i < data.size(); i++) {
			processed.emplace_back((data[i] * 10) / max(data));
		}
	}
};


int main() {
	int limit;
	std::vector<int> data;
	int max_len;
	std::cout << "Enter Limit: " << std::endl;
	std::cin >> limit;
	data.reserve(50);
	for (int i = 1; i <= limit; i++) {
		const char* suffix;
		unsigned int val;
		switch (i) {
		case 1: suffix = "st"; break;
		case 2: suffix = "nd"; break;
		case 3: suffix = "rd"; break;
		default: suffix = "th"; break;
		}
		std::cout << "Enter " << i << suffix << " value: ";
		std::cin >> val;
		data.emplace_back(val);
	}
	data.shrink_to_fit();
	max_len = basic_utils::max(data);
	std::vector<int> processed_data;
	processed_data.reserve(data.size());
	basic_utils::process_data(processed_data, data);
	int dynamic_width = std::to_string(max_len).length();
	for (int i = 1; i < 11; i++)
	{
		std::cout << "|";
		if (dynamic_width == 1)
			dynamic_width += 1;
		for (int j = 0; j < processed_data.size(); j++)
		{
			for (int k = 0; k < dynamic_width; k++) 
				std::cout << (i > 10 - processed_data[j] ? "%" : " ");
			std::cout << " ";
		}
		std::cout << std::endl;
	}
}
