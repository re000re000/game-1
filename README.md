import turtle

#ウィンドウの表示
sc = turtle.Screen()
sc.title("Pong game")
sc.bgcolor("white")
sc.setup(width=1000, height=600)

#左側のバー表示
left_pad = turtle.Turtle()
left_pad.speed(0)
left_pad.shape("square")
left_pad.color("black")
left_pad.shapesize(stretch_wid=6, stretch_len=2)
left_pad.penup()
left_pad.goto(-400, 0)

#右側のバー表示
right_pad = turtle.Turtle()
right_pad.speed(0)
right_pad.shape("square")
right_pad.color("black")
right_pad.shapesize(stretch_wid=6, stretch_len=2)
right_pad.penup()
right_pad.goto(400, 0)

#ボールの表示
hit_ball = turtle.Turtle()
hit_ball.speed(40)
hit_ball.shape("circle")
hit_ball.color("blue")
hit_ball.penup()
hit_ball.goto(0, 0)
hit_ball.dx = 5
hit_ball.dy = -5

# 点数初期値
left_player = 0
right_player = 0

#点数表示
sketch = turtle.Turtle()
sketch.speed(0)
sketch.color("blue")
sketch.penup()
sketch.hideturtle()
sketch.goto(0, 260)
sketch.write("左のプレーヤー : 0 右のプレーヤー: 0",
            align="center", font=("Courier", 24, "normal"))

#左側のバーの動き
def paddleaup():
    y = left_pad.ycor()
    y += 20
    left_pad.sety(y)
    
def paddleadown():
    y = left_pad.ycor()
    y -= 20
    left_pad.sety(y)

#右側のバーの動き
def paddlebup():
    y = right_pad.ycor()
    y += 20
    right_pad.sety(y)

def paddlebdown():
    y = right_pad.ycor()
    y -= 20
    right_pad.sety(y)

#キーボード操作の情報
sc.listen()
sc.onkeypress(paddleaup, "w")
sc.onkeypress(paddleadown, "c")
sc.onkeypress(paddlebup, "Up")
sc.onkeypress(paddlebdown, "Down")

while True:
    sc.update()

    hit_ball.setx(hit_ball.xcor()+hit_ball.dx)
    hit_ball.sety(hit_ball.ycor()+hit_ball.dy)

    #加点条件
    if hit_ball.ycor() > 280:
        hit_ball.sety(280)
        hit_ball.dy *= -1

    if hit_ball.ycor() < -280:
        hit_ball.sety(-280)
        hit_ball.dy *= -1

    if hit_ball.xcor() > 500:
        hit_ball.goto(0, 0)
        hit_ball.dy *= -1
        left_player += 1
        sketch.clear()
        sketch.write("左のプレーヤー : {} 右のプレーヤー: {}".format(
            left_player, right_player), align="center",
            font=("Courier", 24, "normal")
        )

    if hit_ball.xcor() < -500:
        hit_ball.goto(0, 0)
        hit_ball.dy *= -1
        right_player += 1
        sketch.clear()
        sketch.write("左のプレーヤー : {} 右のプレーヤー: {}".format(
            left_player, right_player), align="center",
            font=("Courier", 24, "normal")
        )

    #バーに当たった時の処理
    if ( hit_ball.xcor()>360 and hit_ball.xcor()<370) and (hit_ball.ycor()<right_pad.ycor()+40 and hit_ball.ycor()>right_pad.ycor()-40):
        hit_ball.setx(360)
        hit_ball.dx*=-1
        
    if (hit_ball.xcor()<-360 and hit_ball.xcor()>-370) and (hit_ball.ycor()<left_pad.ycor()+40 and hit_ball.ycor()>left_pad.ycor()-40):
        hit_ball.setx(-360)
        hit_ball.dx*=-1
