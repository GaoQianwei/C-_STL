# STL_打分案例

评委打分案例(sort 算法排序)

- 创建 5 个选手(姓名，得分) ， 10 个评委对 5 个选手进行打分
- 得分规则：去除最高分，去除最低分，取出平均分
- 按得分对 5 名选手进行排名

```cpp
#define _CRT_SECURE_NO_WARNINGS
#define PLAYER_NUMBER 5
#include<iostream>
#include<string>
#include<vector>
#include<deque>
#include<algorithm>
#include<stdlib.h>
#include<time.h>
using namespace std;

//选手类
class Player {
public:
	Player() {};
	Player(string name, int score){
		this->name = name;
		this->score = score;
	}
	string getName() {
		return this->name;
	}
	void setName(string name) {
		this->name = name;
	}
	int getScore() {
		return this->score;
	}
	void setScore(int score) {
		this->score = score;
	}
private:
	string name;
	int score;
};

void creat_player(vector<Player> &player_vector,int number) {
	string name_seed = "ABCDE";
	for (int i = 0; i < number; i++) {
		Player player;
		string tmp = name_seed.substr(i,1);
		player.setName("选手"+tmp);
		player.setScore(0);
		player_vector.push_back(player);
	}
}

void set_score(vector<Player>& player_vector) {
	
	srand(time(nullptr));

	for (vector<Player>::iterator it=player_vector.begin();it!=player_vector.end();it++) {
		
		deque<int> player_score_list;
		
		for (int i = 0;i<10;i++) {
			int score = rand() % 41 + 60;
			player_score_list.push_back(score);
		}
		
		sort(player_score_list.begin(),player_score_list.end());
		
		player_score_list.pop_back();
		player_score_list.pop_front();

		int total_score = 0;
		for (deque<int>::iterator dit = player_score_list.begin(); dit != player_score_list.end(); dit++) {
			total_score += (*dit);
		}
		int avg_score = total_score / player_score_list.size();

		(*it).setScore(avg_score);
	}
}

bool mycompare(Player& p1, Player& p2) {
	return p1.getScore() > p2.getScore();
}

void print_rank(vector<Player>& player_vector) {

	sort(player_vector.begin(),player_vector.end(),mycompare);

	for (vector<Player>::iterator it = player_vector.begin(); it != player_vector.end(); it++) {

		cout << "姓名："<<(*it).getName()<<"  得分："<<(*it).getScore()<<endl;
	}
}


int main()
{
	vector<Player> player_vector;
	creat_player(player_vector,PLAYER_NUMBER);
	set_score(player_vector);
	print_rank(player_vector);
	return 0;
}
```

