unit MainForm;

interface

uses
  Winapi.Windows, Winapi.Messages, System.SysUtils, System.Variants, System.Classes, Vcl.Graphics,
  Vcl.Controls, Vcl.Forms, Vcl.Dialogs, Vcl.StdCtrls, Vcl.ExtCtrls;

type

  TWin8Control = class(TButton)
  private
    WinBitMap: TBitMap;
  public
    procedure CreateWnd; override;
    constructor Create(AOWner: TComponent; BitMap: TBitMap);
  end;

  TfrmMain = class(TForm)
    Image: TImage;
    btnAdd100: TButton;
    procedure btnAdd100Click(Sender: TObject);
  private
    { Private declarations }
  public
    { Public declarations }
  end;

var
  frmMain: TfrmMain;

implementation

{$R *.dfm}

{ TWin8Control }

constructor TWin8Control.Create(AOWner: TComponent; BitMap: TBitMap);
begin
  inherited Create(AOwner);
  WinBitMap := BitMap;
end;

procedure TWin8Control.CreateWnd;
var
  bf: TBlendFunction;
  BitmapSize: TSize;
  BitmapPos:Tpoint;
begin
  inherited;

  // убеждаемся в том что у нас Premultiplied битмап
  WinBitMap.AlphaFormat := afPremultiplied;

  bf.BlendOp := AC_SRC_OVER;
  bf.BlendFlags := 1;
  bf.AlphaFormat := AC_SRC_ALPHA;
  bf.SourceConstantAlpha := 255;
  // получаем размеры BitMap
  BitmapSize.cx := WinBitMap.Width;
  BitmapSize.cy := WinBitMap.Height;
  BitmapPos.X := 0;
  BitmapPos.Y := 0;
  // добавляем "слоистый" стиль окна
  SetWindowLong(Handle, GWL_EXSTYLE, GetWindowLong(Handle, GWL_EXSTYLE) or WS_EX_LAYERED);
  UpdateLayeredWindow(
    Handle,
    0,
    nil,
    @BitmapSize,
    WinBitMap.Canvas.Handle,
    @BitmapPos,
    0,
    @bf,
    ULW_ALPHA
  );
end;

procedure TfrmMain.btnAdd100Click(Sender: TObject);
var
  i: Integer;
  Win8Control: TWin8Control;
begin
  for i := 0 to 99 do
  begin
    Win8Control := TWin8Control.Create(Self, Image.Picture.Bitmap);
    Win8Control.Parent := Self;
    Win8Control.Top := Random(400);
    Win8Control.Left := Random(400);
  end;
end;

end.
